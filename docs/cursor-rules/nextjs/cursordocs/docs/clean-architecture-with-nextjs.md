# Implementación Clean Architecture con Next.js

Utilizar el siguiente enfoque para mantener separación de las capas de datos, lógica de negocio y UI:

1. Entidades: Representan los modelos de datos.
2. Servicios: Se encargan de la interacción con la base de datos.
3. Casos de Uso: Contienen la lógica de negocio pura.
4. Server Actions: Son puntos de entrada para mutaciones desde la UI.
5. Zustand: Maneja el estado local solo cuando es necesario.

Con esta estructura, se podrá escalar fácilmente la aplicación sin generar deuda técnica.

## Plan de Implementación

El siguiente plan de implementación es una guía para crear una aplicación de notas con una arquitectura basada en Clean Architecture usando Next.js, Drizzle, Zustand, React Server Components y Clerk para la autenticación.

### 1. Definir la Entidad Note

La entidad solo define la estructura de los datos.

```typescript
// src/entities/note.ts
export interface Note {
  id: string
  userId: string
  title: string
  content: string
  createdAt: Date
  updatedAt: Date
}
```

### 2. Crear el Servicio para manejar la base de datos

Este servicio interactúa con Drizzle para manejar la persistencia.

```typescript
// src/services/note-service.ts
import { db } from "@/lib/drizzle"
import { notes } from "@/lib/schema"
import { eq } from "drizzle-orm"

export const NoteService = {
  async getNotes(userId: string) {
    return db.select().from(notes).where(eq(notes.userId, userId))
  },

  async createNote(userId: string, title: string, content: string) {
    return db.insert(notes).values({ userId, title, content }).returning()
  },

  async updateNote(
    userId: string,
    noteId: string,
    title: string,
    content: string
  ) {
    return db
      .update(notes)
      .set({ title, content })
      .where(eq(notes.id, noteId) && eq(notes.userId, userId))
  },

  async deleteNote(userId: string, noteId: string) {
    return db
      .delete(notes)
      .where(eq(notes.id, noteId) && eq(notes.userId, userId))
  }
}
```

### 3. Crear los Casos de Uso

Aquí encapsulamos la lógica de negocio sin acoplarla a la UI ni a la base de datos.

```typescript
// src/use-cases/notes/create-note.ts
import { NoteService } from "@/services/note-service"
import { z } from "zod"

const noteSchema = z.object({
  title: z.string().min(1),
  content: z.string().min(1)
})

export async function createNote(
  userId: string,
  title: string,
  content: string
) {
  const validatedData = noteSchema.parse({ title, content })
  return NoteService.createNote(
    userId,
    validatedData.title,
    validatedData.content
  )
}
```

### 4. Implementar Server Actions

Las mutaciones de la UI deben usar server actions para mantener la lógica en el servidor.

```typescript
// src/app/(dashboard)/notes/actions.ts
"use server"

import { createNote } from "@/use-cases/notes/create-note"
import { auth } from "@clerk/nextjs"

export async function createNoteAction(formData: FormData) {
  const user = auth()
  if (!user) throw new Error("Unauthorized")

  const title = formData.get("title") as string
  const content = formData.get("content") as string

  await createNote(user.id, title, content)
}
```

### 5. Crear la UI con React Server Components

La UI usa los server actions y Zustand para actualizar el estado local.

```typescript
// src/app/(dashboard)/notes/page.tsx
"use client"

import { useState } from "react"
import { createNoteAction } from "./actions"
import { useNoteStore } from "@/stores/note-store"

export default function NotesPage() {
  const [title, setTitle] = useState("")
  const [content, setContent] = useState("")
  const { notes, fetchNotes } = useNoteStore()

  async function handleCreateNote() {
    await createNoteAction(
      new FormData().append("title", title).append("content", content)
    )
    fetchNotes() // Refrescar estado local
  }

  return (
    <div>
      <h1 className="text-xl font-bold">My Notes</h1>
      <input
        type="text"
        value={title}
        onChange={(e) => setTitle(e.target.value)}
      />
      <textarea value={content} onChange={(e) => setContent(e.target.value)} />
      <button onClick={handleCreateNote}>Create Note</button>

      <ul>
        {notes.map((note) => (
          <li key={note.id}>
            <h2>{note.title}</h2>
            <p>{note.content}</p>
          </li>
        ))}
      </ul>
    </div>
  )
}
```

## Análisis de mejora

Realizando un Análisis de Mejora se identifican los siguientes aspectos a mejorar:

1. Lo que está bien: ✅ Uso de Clean Architecture con separación clara de responsabilidades.

- ✅ Uso de React Server Components y Server Actions para lógica en el servidor.
- ✅ Uso de Drizzle ORM, una opción ligera y eficiente para bases de datos en Next.js.
- ✅ State Management con Zustand es una elección correcta para UI reactiva.

2. Lo que se puede mejorar: ❌ Error handling más detallado y con errores de dominio específicos.

- ❌ Validaciones más estrictas con Zod para evitar datos incorrectos.
- ❌ Mejor comunicación de errores entre la API y la UI.
- ❌ Estado optimizado con actualizaciones inmediatas en el frontend.

## 1️. Error Handling (Manejo de Errores)

El manejo de errores es crucial en cualquier aplicación, y hay varias áreas donde puede mejorar:

1. 📌 Problemas Identificados

- Falta de manejo de errores en el servicio (NoteService). Actualmente, si una consulta falla, se lanzará un error genérico de Drizzle.
- Falta de manejo de errores en los casos de uso (createNote). Si la validación de Zod falla, no se maneja el error.
- Falta de manejo de errores en las server actions (createNoteAction). Si createNote falla, no se devuelve un mensaje de error útil.

2. ✅ Soluciones

- Envolver las funciones del servicio en try/catch y lanzar errores de dominio personalizados.
- Capturar y manejar errores en los casos de uso para enviar respuestas más descriptivas.
- Enviar errores estructurados desde las server actions a la UI.

#### ✨ Ejemplo Mejorado de Manejo de Errores

```typescript
// src/services/note-service.ts
import { db } from "@/lib/drizzle"
import { notes } from "@/lib/schema"
import { eq } from "drizzle-orm"

export const NoteService = {
  async getNotes(userId: string) {
    try {
      return await db.select().from(notes).where(eq(notes.userId, userId))
    } catch (error) {
      throw new Error(`Error retrieving notes: ${error}`)
    }
  },

  async createNote(userId: string, title: string, content: string) {
    try {
      return await db
        .insert(notes)
        .values({ userId, title, content })
        .returning()
    } catch (error) {
      throw new Error(`Error creating note: ${error}`)
    }
  },

  async updateNote(
    userId: string,
    noteId: string,
    title: string,
    content: string
  ) {
    try {
      return await db
        .update(notes)
        .set({ title, content })
        .where(eq(notes.id, noteId) && eq(notes.userId, userId))
    } catch (error) {
      throw new Error(`Error updating note: ${error}`)
    }
  },

  async deleteNote(userId: string, noteId: string) {
    try {
      return await db
        .delete(notes)
        .where(eq(notes.id, noteId) && eq(notes.userId, userId))
    } catch (error) {
      throw new Error(`Error deleting note: ${error}`)
    }
  }
}
```

### 2️. Best Practices

#### Separación de Errores de Dominio

En lugar de lanzar errores genéricos (throw new Error("Error creando nota")), puedes definir errores de dominio específicos:

```typescript
export class NoteCreationError extends Error {
  constructor(message = "Failed to create note") {
    super(message)
    this.name = "NoteCreationError"
  }
}
```

Luego, puedes usarlo en NoteService:

```typescript
catch (error) {
  throw new NoteCreationError()
}
```

#### Mejor Validación con Zod en el Caso de Uso

El esquema de validación de Zod debería manejar más casos de error:

```typescript
const noteSchema = z.object({
  title: z.string().min(1, "Title is required").max(100, "Title too long"),
  content: z
    .string()
    .min(1, "Content is required")
    .max(1000, "Content too long")
})

export async function createNote(
  userId: string,
  title: string,
  content: string
) {
  try {
    const validatedData = noteSchema.parse({ title, content })
    return await NoteService.createNote(
      userId,
      validatedData.title,
      validatedData.content
    )
  } catch (error) {
    if (error instanceof z.ZodError) {
      throw new Error(error.errors.map((e) => e.message).join(", "))
    }
    throw new Error("Unexpected error while creating note")
  }
}
```

#### Mejora en createNoteAction para Enviar Mensajes de Error a la UI

Si el caso de uso lanza un error, debe devolverse a la UI de forma clara:

```typescript
export async function createNoteAction(formData: FormData) {
  try {
    const user = auth()
    if (!user) throw new Error("Unauthorized")

    const title = formData.get("title") as string
    const content = formData.get("content") as string

    await createNote(user.id, title, content)
    return { success: true }
  } catch (error) {
    return { success: false, message: error.message || "Something went wrong" }
  }
}
```

En la UI, puedes capturar estos errores:

```typescript
async function handleCreateNote() {
  const response = await createNoteAction(
    new FormData().append("title", title).append("content", content)
  )

  if (!response.success) {
    alert(response.message) // O mejor, crear un componente de error para mostrarlo en la UI
  } else {
    fetchNotes()
  }
}
```

### 3️. Mejoras en la UI con un Estado Global Más Óptimo

El estado global con Zustand podría simplificarse para mejorar la experiencia del usuario:

```typescript
import { create } from "zustand"

interface NoteState {
  notes: Note[]
  fetchNotes: () => Promise<void>
  addNote: (note: Note) => void
}

export const useNoteStore = create<NoteState>((set) => ({
  notes: [],
  fetchNotes: async () => {
    const res = await fetch("/api/notes") // Crear una API handler
    const data = await res.json()
    set({ notes: data })
  },
  addNote: (note) => set((state) => ({ notes: [...state.notes, note] }))
}))
```

#### Mejor integración en la UI:

```typescript
async function handleCreateNote() {
  const response = await createNoteAction(
    new FormData().append("title", title).append("content", content)
  )

  if (!response.success) {
    alert(response.message)
    return
  }

  useNoteStore.getState().addNote(response.note) // Estado local inmediato
}
```
