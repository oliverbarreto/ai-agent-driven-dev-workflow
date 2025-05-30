# TODOs

## DAILY WORK

### 20250205

- [x] Modificada la navegación para que sea responsive
- [x] Añadida la navegación móvil (Shadcn drawer and burger menu) y separada de la de escritorio
- [x] Corregidos errores de layout en mobile (páginas, barchart, ...)

### 20250206

- [x] Refactor de Estructura de Páginas
- [x] BUG: Arreglar la entrada de datos en mobile
- [x] BUG: Arreglar el aspecto del sidebar en mobile
- [x] BUG: Arreglar el aspecto de los componentes de la página /registros en mobile

### 20250208

- [x] Refactor: Continuar con la modificación de Modelo de datos de usuarios para ampliar la información de los los registros de eventos de los usuarios y añadir cancelaciones de eventos. CONTEXT: the full epic task is described in the @prd_v2.md file.
- [x] Nuevo código de cálculo de la jornada de trabajo: clock-in y clock-out, y tipo de actividad (trabajo, formación, pausa, comida, desayuno, otros)
- [x] Nuevo código de lógica de registros e incidencias (registros a posterior o a priori de eventos de trabajo)
- [x] Extraído formulario de registro de eventos a un componente independiente
- [x] Terminada Pantalla TODAY
- [ ] Modificada la pantalla de Event Registration: Cálculo de "first start" y "last end" de la jornada de trabajo (work and training)

### 20250209

- [x] Add functionality to add pagination to the time entries table (use tankstack for pagination)
- [x] UI: Cambio en el orden de las columas de la tabla de "time-entries": user, date, type, concept, is_incidence (Yes/No), device, location, notes, y para hacer el campo "is_incidence" sortable (Yes/No)
- [x] Terminar Pantalla de Barcharts
- [x] Arreglado BUG que hacía que el se mostrara dos veces el contenido de cada página en el layout en mobile
- [x] Arreglado BUG con padding top en el layout en mobile
- [x] Corregir errores de Linting y Building para subir a Vercel

- [x] Añadido espacio para que las páginas en el layout tengan un padding top con el navbar en mobile
- [x] Refactor model and logic of time tracking system with new requirements in prd_v2.md (cancelations, new fields in time_entries table, etc.)
- [x] Refactor time tracking system with clock-in and clock-out work time and break time
- [x] Refactor logic to calculate the total time worked in a day
- [x] Refactor pages and components to use the new model and logic of time tracking system

  - [x] Refactor page design for Event Registration Control Panel
  - [x] Refactor app structre for registering daily hours
  - [x] Revisar y Refactor graphs to display time worked in a day, week, month, year, etc.
  - [x] Revisar y Refactor de la app structre y de la página de tabla de registros de horas (/registros) para que se pueda filtrar por fecha y por tipo (start, end) y concepto de registro (trabajo, formación, almuerzo, médico, otro, etc.)

- [x] Terminar Pantalla Today
- [x] Terminar Pantalla de Registros

### 20250210

- [x] Add new functionality to mark time entries as "cancelled"

  - [x] Hacer funcionalidad de cancelar un registro de horas (Analizar si hay que modificar el modelo de datos de la tabla time_entries con una columna "is_cancelled", en lugar de la tabla actual relacionada con las cancelaciones).
    - [x] RESULTADO: Mejor no tocar la tabla de "time_entry_cancellation" por ahora. Seguimos con la tabla relacionada con las cancelaciones.
  - [x] Analyze the current schema in which we have "time_entries" table and "time_entry_cancellation" table to create logic and actions to access the data required to provide the new feature.
  - [x] Add new functionality to allow the user to cancel "time-entries" from:

    - [x] 1. from the list of events registered for current date in the component "current-day.tsx" in the page "/jornada"
    - [x] 2. from the table with time entries with in the component "time-entries-table.tsx" in the page "/registros"

- [x] BUG: Modificar el layout de los controles de paginación para mobile
- [x] UI: Mejora diseños de la página de "time-entries-control-panel" para alinear a la izquierda las estadísticas
- [x] Test pagination feature with tankstack

### 20250211

- [x] Mapas y Localización según `prd_v4.md`:
  - [x] Añadida funcionalidad de localización en mapas a la tabla de registro de horas (/registros) para permitir ver la localización de cada registro de horas.
  - [x] Creado proyecto en Google Cloud Console y obtenido API key para utilizar Google Maps API.
  - [x] Instalado y configurado `@react-google-maps/api` para utilizar Google Maps API (npm install --save @react-google-maps/api)
  - [x] Añadido el API key en el archivo `.env.local` en la variable `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY`.
  - [x] BUG FIX: añadido `<DialogDescription className="hidden">{title}</DialogDescription>` en el componente `MapModal.tsx` para evitar error de `aria-description` not present in the component.

Phase 4: New functinoality to create "Recent Absences" component.

- [x] Added new service to work with mockuser for development purposes.
- [x] Add new functionality to create a new "Incidence List" component. We should divide this component into two sections:

  - [x] Recent Absences: It should display a list of all "absences" for the current user: that is days without any time entry at all;
  - [x] Uncompleted Days: which are dates with at least one unfinished session, work/training or any other type, lunch, medical, break, other, etc.

### 20250212

- [x] BUG FIX: depurar errores del linter y del builder `npm run build`

  - [x] Add misisng Import to `button.tsx` to be able to use the component: `import React from "react"`

  - [x] BUG FIX: Type error in `uncompleted-days-list.tsx` and `recent-absences-list.tsx`.
    - [x] Let's add it to `uncompleted-days-list.tsx` This adds proper typing for the onRegisterTimeEntry callback prop with the correct parameter types. I made it optional with ? since it's not used in all instances of the component.`import { TimeEntryConcept } from "@/types"`
    - [x] Solved the error by removing the onRegisterTimeEntry prop from both components since it is not needed for the components to work.

  ```
  Error occurred prerendering page "/incidencias". Read more: https://nextjs.org/docs/messages/prerender-error
  Error: Event handlers cannot be passed to Client Component props.
    {date: Date, onRegister: function onRegisterTimeEntry}
                             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  If you need interactivity, consider converting part of this to a Client Component.
      at e$ (/Users/oliver/dev/ai/fichajes/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:84:23556)
      at Object.toJSON (/Users/oliver/dev/ai/fichajes/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:84:14874)
      at stringify (<anonymous>)
      at eU (/Users/oliver/dev/ai/fichajes/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:84:26231)
      at eB (/Users/oliver/dev/ai/fichajes/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:84:26461)
      at eq (/Users/oliver/dev/ai/fichajes/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:84:27015)
      at Immediate._**onImmediate** (/Users/oliver/dev/ai/fichajes/node_modules/next/dist/compiled/next-server/app-page.runtime.prod.js:84:14577)
      at process.processImmediate (node:internal/timers:480:21)
      at process.callbackTrampoline (node:internal/async_hooks:130:17)
  Export encountered an error on /(users)/incidencias/page: /incidencias, exiting the build.
   ⨯ Static worker exited with code: 1 and signal: null
  ```

  - [x] This change should resolve the type error. I've:
    1. Imported the TimeEntryConcept type from @/types
    2. Updated the concept field in the unfinishedSessions array to use TimeEntryConcept instead of string
    3. Now TypeScript will ensure that only valid concepts ("work", "training", "break", "lunch", "medical", or "other") are passed to the TimeEntryDialog component.
  - [x] These changes should resolve the type error by:
    1. Creating a shared UncompletedDay type in src/types/uncompleted-day.ts
    2. Updating both the action and component to use this shared type
    3. Properly typing the concept as TimeEntryConcept in the action
    4. Adding the type to the exports in src/types/index.ts
    5. The type error should now be resolved, and both components will be using the same type definition.

- [x] UI: SIDEBAR - Make it so as soon as the user clicks a menu option of the sidebar the sidebar should hide
- [x] UI: la celda cada evento en "curren-day.tsx" /jornada, debe mostrar, aparte de grayed out, "Cancelled" as text. Poner los eventos como "badge pills"
- [x] BUG FIX: linting errors in all app after adding the incidence list and recent absences components
- [x] BUG: /jornada - event-registration-control-panel.tsx: Revisar como se calculan las estadísticas de first start y last end en la pantalla de "Jornada de trabajo", porque para el caso de haber metido un registro el día antes (por ejemplo) como incidencia, aparece que tengo el evento en la lista de eventos del día pero no aparece la hora en "first start". (First Start: No entries, Last End: No entries). Quizás están calculadas a partir de la hora de creación en lugar del timestamp del registro.
  - [x] SOLUTION: no hay error. El comportamiento es el esperado ya que el caso revisado la entrada estaba cancelada. Por tanto, no hay eventos sin cancelar para calcular los estadísticos de first start y last end, y por eso no hay entradas.

### 20250213

- [x] USERS with CLERK: Refactor current functionality to work with current logged in user with Clerk
  - [x] BUG FIX: Solventado error de layout de todos los componentes al añadir Clerk. Era provocado por el Provider de Google API en el layout. en concreto hay que comentar la línea `// preventGoogleFontsLoading // Prevent loading additional Google Fonts`

Completed initial Clerk setup:

- [x] Project created in Clerk dashboard
- [x] Environment variables configured
- [x] Middleware setup
- [x] ClerkProvider added to layout

Schema updates completed:

- [x] Added new enums for user roles and status
- [x] Updated Organizations table with additional fields
- [x] Updated Users table with Clerk integration
- [x] Updated Departments table with additional fields
- [x] Added TypeScript types for better type support

Authentication UI components created:

- [x] Created UserNav component with Clerk's SignIn and UserButton
- [x] Created UserAvatar component for profile display
- [x] Integrated auth components in both desktop and mobile navigation
- [x] Added proper role-based UI states (SignedIn/SignedOut)

### 20250214

- [x] Añadir tabla de Locations (Centros de Trabajo) para almacenar las distintas localizaciones de la organización. Los usuarios prodrán ahora pertenecer a un centro y a un departamento.

  - [x] Cada centro tendrá:
    - [ ] id (string cuid) @unique
    - [ ] nombre (string)
    - [ ] slug String @unique
    - [ ] localizacion? (latitud y longitud) (opcional)
    - [ ] direccionPostal? (calle, número, piso, puerta, código postal, ciudad, provincia, país).
    - [ ] telefono? (opcional)
    - [ ] email? (opcional)
    - [ ] horario de atención (hora de inicio y hora de fin de la jornada de atención al público) (opcional)
    - [ ] zona horaria del centro (UTC, CET, Atlantic/Canary, etc.)
    - [ ] created_at
    - [ ] updated_at

- [x] Crear Pantallas y Servicios CRUD para Organización
- [x] Crear Pantallas y Servicios CRUD para Centros
- [x] Crear Pantallas y Servicios CRUD para Departamentos
- [x] Crear Pantallas y Servicios CRUD para Usuarios
- [x] Crear Pantallas y Servicios CRUD para Roles
- [x] Crear Pantallas y Servicios CRUD para Permisos

- [x] REFACTOR: Añadida comprobación en los Webhooks de Clerk para que se pueda crear el primer usuario de la organización con permisos de rol de administrador "admin" y status "active".
- [x] FEATURE - SCHEMA: Añadida la tabla de Locations (Centros de Trabajo) para almacenar las distintas localizaciones de la organización. Los usuarios prodrán ahora pertenecer a un centro y a un departamento.
- [x] REFACTOR - UI: "detour" de la modificación de la navegación y la reestructuración de las páginas de marketing, para volver a retomar la funcionalidad de la app principal

- [x] USERS with CLERK: Refactor current functionality to work with current logged in user with Clerk

### 20250215

- [x] Refactor current functionality to work with current logged in user with Clerk - Phase 5.6: Refactor functionality of current (admin) routes: /admin, /admin/company, /admin/locations, /admin/departments to work with current logged in user with Clerk
  - [x] 1. Refactor for routes: /admin, /admin/company, /admin/locations, /admin/departments
- [x] BUGFIX: arreglado problema de múltiples layouts en la app: app, auth, marketing, users, admin ...

### 20250216

- [x] REFACTOR: We now want to add some Busines Rules that affect the UI. Please thoroughly analyze the logic in charge and change it accordingly to meet the next requirements. REQUIREMENTS:

  - [x] Modify the sidebar so that on mobile all the links for "/admin/\*" routes are shown in the menu only when the logged-in userhas the "admin" role. Right now the links work but they show the "/unauthorized" page for all admin routes, when the links should not be shown in the menu.
  - [x] We need to make it work for both, the mobile and desktop sidebar, since we distinguish between them in the component in charge of navigation.
  - [x] The navigation bar now shows a drawer from the bottom of the screen for mobile devices. It now uses a different height depending on the role of the user logged in, and shows the links for the routes "/admin/\*" only when the user has the "admin" role. It also has a subtle pane at the bottom with the user button, the dark mode toggle and the settings page button.

- [x] Add Admin Busines Rules: an admin user cannot delete its own user account
- [x] BUGFIX UI: arreglar el layout de las páginas de (marketing) que se había roto y no estaba centrado el contenido.
- [x] REFACTOR: Modificar el sidebar para que no se muestre el título de la sección "App", solo para Adminla opción de "admin" dashboard en el caso de que el usuario no tenga permisos de administrador. Ahora mismo funciona pero redirige a la página
- [ ] REFACTOR UI: modificar el sidebar para añadir un botón de expandir/contraer, el efecto de automatismo está bien, pero afecta la UX ya que posiciona el cursor en otro menú al expandir.
- [x] REFACTOR UI: Poner pestaña de "Días incompletos" primero, y después la pestaña de "ausencias" en la página de /incidencias
- [x] REFACTOR UI: modificar la UI de /jornada, para añadir links que lleven a /incidencias

  - I've completed the implementation of the navigation buttons in the DashboardHeader component. Here's what I've done:
    - Added two navigation buttons:
      - "Incidencias" button with an AlertTriangle icon
      - "Registros" button with a FileText icon
    - Implemented responsive layout:
      - On mobile devices, the buttons stack vertically in a column below the user info
      - On desktop devices, the buttons align horizontally in a row on the right side
    - Used Shadcn components and styling:
      - Used Shadcn Button component with outline variant
      - Used Lucide icons for visual consistency
    - Maintained the existing Card and CardHeader components
    - Kept existing functionality:
      - User avatar and info display remains unchanged
      - All existing features continue to work as before
    - The implementation follows the requirements exactly, focusing only on adding the navigation buttons while maintaining the existing design and functionality. The layout is mobile-friendly and adapts well to different screen sizes.

- [x] REFACTOR: Refactor to solve build errors
- [x] Phase 5.7: Refactor functionality of current (users) routes: /jornada, /incidencias, /registros to work with current logged in user with Clerk

  - [x] 1. Refactor the app functionality for routes (/jornada, /incidencias, /registros) under the folder (users) to work with the current logged in user via Clerk authentication

    - [x] Modify the server actions to work with the current logged in user
    - [x] Modify the client components to work with the current logged in user
    - [x] Modify the server components to work with the current logged in user

  - [x] 2. Test the functionality of the routes (/jornada, /incidencias, /registros) under the folder (users) to work with the current logged in user via Clerk authentication

- > IMPORTANT NOTE:
  >
  > 1. Do not modify the functionality of the (admin) routes (/admin, /admin/company, /admin/locations, /admin/departments)
  > 2. Do not modify the UI or design, just the functionality

- [x] Refactor linter errors for deployment in production
- [x] update documentation for phase 5.6 and 5.7

### 20250217

- [x] REFACTOR FEATURE: Ahora el comportamiento de la página de "/admin/users" permite asignar un usuario a un departamento/equipo. Hay que revisar el código para ver si hace falta refactorizar alguna parte y mejorar seguridad y las server actions; y si hace falta añadir Tankstack para las queries y validar casos de error.
- [x] FEATURE: Se añade una nueva Buisess Rule: Ahora un usuario admin no puede bloquearse a sí mismo
- [x] REFACTOR UI: Extraída la funcionalidad y los componentes de interfaz de usuario de las estadísticas "First Start" y "Last Start" que ahora se muestran en el componente "event-registration-control-panel.tsx" y muévalos al componente "current-day.tsx".
- [x] REFACTOR UI: Agreguegado más espacio por abajo hasta el componente con el botón de usuario, el botón de alternancia del modo oscuro y el enlace a la página de configuración. Necesitamos más espacio para respirar
- [x] REFACTOR UI: Agreagado más espacio al botón de alternancia de la barra lateral cuando esté contraída. Tiene que estar en el mismo lugar donde está el botón cuando la barra lateral está expandida.
- [x] REFACTOR UI: Eliminado el separador de la sección de menú Admin cuando el sidebar está contraido
- [x] REFACTOR UI: Añadida funcionalidad para hacer que el icono de reloj sea un botón para actualizar la página con las horas.
- [x] REFACTOR UI: Modificada la UI del componente "event-registration-control-panel.tsx" para hacer responsible los botones de acción con el layout de la página para dispositivos medianos
- [x] REFACTOR UI: Mover combo de opción de gráfico y ponerlo debajo del total de horas alineado a la izquierda.
- [x] REFACTOR UI: Añadido botón de refresh gráfica de estadísticas en "/jornada"

### 20250218

- [x] BUGFIX: arreglado el problema con el cálculo de días incompletos que había dejado de funcionar.
  - [ ] Estaba teniendo en cuenta los registros de tiempo caneelados en el algoritmo. Ahora filtra las canceladas al principio, y pasa el resto por el algoritmo de segmentos.
  - [ ] no estaba teniendo en cuenta que un día puede tener varios segmentos de registro de tiempo (por ejemplo, puede empezar a trabajar en un centro y después irse a otro distinto). Ahora tiene en cuenta los segmentos de tiempo y los suma para calcular el total de días incompletos.
- [x] Se configura en Clerk la nueva ruta para `/api/webhooks/clerk` para trabajar con el nuevo dominio de Vercel `fichajes.oliverbarreto.com`
- [x] Deploy en nuevo proyecto Vercel para poder poner el SECRET_SIGNING enviaronment variable necesaria para poder trabajar con Clerk.
- [x] Para poder hacer el deploy en Vercel y trabajar con Clerk, es necesario añaidur un dominio que no sea "vercel.app". Creada una ruta en oliverbarreto.com y se crean entradas CNAME en el DNS del dominio. Se crea `fichajes.oliverbarreto.com`

### 20250219

- [x] Corregidos errores detectados en el testeo de la funcionalidad de (users) routes: /jornada, /incidencias, /registros & (admin) routes: /admin, /admin/users, /admin/company, /admin/locations, /admin/locations/locationId, /admin/departments, /admin/departments/departmentId

  - [x] TODO: ✅ BUGFIX: el botón de refresh debe resetear los filtros a sus valores por defecto, solo resetea el filtro de fecha
  - [x] TODO: ✅ BUGFIX: el nombre de usuario no se muestra en el listado de registros (Unknown)
  - [x] TODO: ✅ BUGFIX: revisar si se está almacenando bien la localización donde se hace el registro
  - [ ] TODO FEATURE: añadir opciones preconfiguradas para el filtro de fechas: hoy, esta semana, semana pasada, este mes, mes pasado, este año.

  - [ ] "/incidencias"

    - [x] TODO: ✅ BUGFIX: se están calculando mal los días incompletos para el usuario actual

  - [ ] "/admin/users"

    - [x] TODO: ✅ BUGFIX: el formulario ahora funciona como se esperaba, pero hay un problema. Como puede ver en la imagen, tenemos un error de validación de restricción. No permite eliminar un usuario ya que el usuario tiene entradas en la tabla de entradas de tiempo en la base de datos. Sin embargo, el usuario administrador debería poder eliminar al usuario del sistema. Esto significa que debe estar seguro, de ahí el cuadro de diálogo de confirmación, para advertir que TODOS LOS REGISTROS asociados con el usuario también se eliminarán.

    AHORA ELIMINAR UN USUARIO SIGNIFICA "BLOQUEAR" al usuario.

    En este punto de la aplicación NO se va a eliminar el usuario, solo se va a bloquear. Hay que pensar qué funcionalidad se quiere tener para los registros:

    - Se elimina todo y nunca más se accede al usuario ni a sus registros del sistema. La empresa puede querer acceder al histórico de trabajo de un usuario ?
    - Se elimina el usuario per se, pero se mantiene el historial de registros ?

    - [x] TODO: ✅ BUGFIX: managers cannot access "/admin/users" page, and they cannot assign users to departments
    - [x] TODO: ✅ BUGFIX: no se puede acceder al modal que permite asignar un usuario a un departamento en /admin/users
    - [x] TODO: ✅ FEATURE: falta añadir opción de eliminar usuario de departamento en /admin/users desde la tabla de usuarios. Dejarlo sin departamento (es opcional). Ya está incluida en la opción de "Asignar usuario a un departamento", simplemente seleccionando "Sin departamento"

  - [x] "/admin/locations"

    - [x] TODO: ✅ BUGFIX: hay que añadir un modal de confirmación para eliminar un departamento. Ahora no permite en el caso de que hayan usuarios asignado por constrains de las relaciones de las tablas.

  - [x] "/admin/departments"
    - [x] TODO: ✅ BUGFIX: hay que añadir un modal de confirmación para eliminar un departamento. Ahora no permite en el caso de que hayan usuarios asignado por constrains de las relaciones de las tablas.

- [x] BUGFIX: revisión de erroes de linter y builder
- [x] BUGFIX: Revisión para deploy nueva versión en Vercel
- [x] Realizado testing de la funcionalidad de (users) routes: /jornada, /incidencias, /registros
- [x] Realizado testing de la funcionalidad de (admin) routes: /admin, /admin/users, /admin/company, /admin/locations, /admin/locations/locationId, /admin/departments, /admin/departments/departmentId

### 20250220

- [x] Deploy on Vercel
- [x] npm run build y refactor error de linter y builder
- [x] TODO: FEATURE: crear script para añadir usuarios de prueba a la base de datos
- [x] TODO: FEATURE: añadir paginación a la página de /admin/users

- [x] TODO: FEATURE: Crear página con paginación en la ruta /admin/users/registros en la que un usuario admin pueda ver todos los registros de tiempo de todos los usuarios.

  - [x] TODO: FEATURE: Añadir la ruta /admin/users/registros en el sidebar: mobile y desktop.
  - [x] TODO: FEATURE: Un usuario admin puede cancelar un registro de tiempo de cualquier usuario.

### 20250221

- [x] Configuración de Cursor con nuevas Project Rules
- [x] Documentación de Nextjs y reglas de Clean Architecture
- [x] Arreglado problema de no poder ejecutar comandos de bash en el terminal del Composer de Cursor

- [x] todo-00001: Make the columns of the table in "/admin/users" sortable
  - The page is handling all the filtering, sorting, and pagination on the server side through the getUsers function. My client-side sorting implementation is breaking this by overriding the server-side sorting. Fixed the users table component to remove the client-side sorting and instead add the sorting parameters to the URL. After this major change, search and filter do not break on "/admin/users" on all paginated pages.

Phase 9: ADVANCED FUNCTIONALITY - MEJORAS UI:

- [x] Añadir spinner o "Loading App..." en lugar de "Loading maps..."
- [x] Añadir Favicon correctamente a la app
- [x] Añadir "/admin/users/registros" página de "/admin" con enlaces a las herramientas con cards

Phase 7a: Advanced Functionality - COMENTARIOS

- [x] todo-00002: Add view cancellation reason action to time entries tables

## 20250222

MEJORAS FUNCIONALIDAD "ADMIN/USERS/REGITROS":

- [x] todo-00003: Add user filter to admin time entries page
- [x] todo-00004: Implement CSV export for admin time entries

MEJORAS FUNCIONALIDAD "/REGITROS":

- [x] todo-00005: Add "Register with details" button to /registros page

## 20250223

OTROS:

- [x] BUGFIX: Resuelto problema con Drizzle-Kit que no permitía ejecutar el comando de "generate" ni "migrate" porque hubo un problema con la generación del script de migración de la tabla de time_entries, para añadir el campo de work_mode.

- [x] TODO: FEATURE: Modificado el formulario de registro de entradas de tiempo para utilizar el estilo de radio buttons mejorado (como botones del ejemplo de shadcn/ui para métodos de pago) para el campo de work_mode.
- [x] TODO: FEATURE: Modificado el formulario de registro de entradas de tiempo para utilizar estilo de radio buttons mejorado (como botones del ejemplo de shadcn/ui para métodos de pago) para la opción de "start" y "end" de un registro de tiempo.
- [x] TODO: **FEATURE: Añadida la información de mostrar en el panel de "current-day" la información del valor del work_mode del primer "first start" de la página "/jornada" para mostrar si el usuario está trabajando en remoto o presencial.**

NUEVA FEATURE: USERS / PRESENCIA-EQUIPO !!!

- [x] todo-00006.md

  - [x] TODO: REFACTOR: Add a new concept in the time entries table to register if an employee is working on-premise or teleworking.
  - [ ] TODO: REFACTOR: modify all components that use time_entry_concept to use the new concept `work_mode: "office" and "telework"`
    - [x] FEATURE: Add work mode data to time entries in current day's log in /jornada page
    - [x] FEATURE: Add work mode column to time entries table in /registros page
    - [x] FEATURE: Add work mode display to uncompleted days list in /incidencias
    - [x] FEATURE: Add work mode column to admin time entries table in /admin/users/registros

## 20250224

- [x] TODO: BUGFIX: corregido los errores de linting y builder
- [x] TODO: Subido a Vercel

## 20250227

- [x] TODO: Modificada la UI de /jornada, /registros y /incidencias para mobile y desktop
- [x] TODO: Subido a Vercel

## 20250228

- [x] TODO: BUGFIX: el formulario de "registrar con detalles" no cabe en la pantalla de mobile y no es manejable.
- [x] TODO: UI: la página de /registros necesita varias mejoras de UI/UX:

  - [x] quitar el botón de añadir "registro con detalle" de la fila de botones de acción de los filtros
  - [x] añadir un botón que permita ocultar y mostrar la sección de filtros.
  - [x] los botones de acción de los filtros están muy juntos y necesitan tener espacio para respirar.
  - [x] añadir el filtro para la opción de work_mode (office/remote).
  - [x] modificado el layout de mobile de la tabla de /registros para hacerla más compacta y que la información tenga menos espacio entre columnas y valores

- [x] TODO: BUGFIX: corregido los errores de linting y builder

- [x] TODO: UI: la página de /admin/users/registros necesita varias mejoras de UI/UX. Hacer la sección de filtros igual que la de /registros.

  - [x] los botones de acción de los filtros están muy juntos y necesitan tener espacio para respirar.
  - [x] modificado el layout de mobile de la tabla de /registros para hacerla más compacta y que la información tenga menos espacio entre columnas y valores
  - [x] añadir un botón que permita ocultar y mostrar la sección de filtros.
  - [x] añadir el filtro para la opción de work_mode (office/remote).

- [x] TODO: UI: Añadir label con descripción a botones de user profile, dark mode, settings del sidebar en el layout para desktop. No tocar para mobile
- [x] TODO: BUGFIX: corregido los errores de linting y builder

- [x] TODO: Subido a Vercel

## 20250304

- [x] TODO: UI: Modificar el layout de las páginas de (users) para que el layout y la disposición de las páginas sea el mismo que el de las rutas (admin)/\*
- [x] TODO: Subido a Vercel

- [x] todo-00008.md - NEW FEATURE: "/computo-horas" & "/admin/computo-horas":

Para Usuarios:

- [x] TODO: FEATURE: Añadir una nueva página "computo de horas" para mostrar las horas trabajadas por el usuario actualmente logedin semanalmente durante un periodo de tiempo concreto.

Para Administradores:

- [x] TODO: FEATURE: Replicar la página de "/computo-horas" para crear una nueva página "/admin/computo-horas" que permita a un administrador ver las horas trabajadas por todos los usuarios actualmente logedin semanalmente durante un periodo de tiempo concreto.

- [x] TODO: Corregir errores de Linting y Building para subir a Vercel
- [x] TODO: Subido a Vercel

- [x] BUGFIX: Fix tab selection and data refresh issues in the locations section

  - [x] Fix tab selection after adding/removing users from a location
  - [x] Fix data refresh issues when adding/removing users from a location
  - [x] Ensure available users are properly refreshed in the add member dialog

- [x] BUGFIX: Fix tab selection and data refresh issues in the departments section

  - [x] Fix tab selection after adding/removing users from a department
  - [x] Fix data refresh issues when adding/removing users from a department
  - [x] Ensure available users are properly refreshed in the add member dialog

- [x] NEW FEATURE: Añadir página de "/admin/settings"
- [x] TODO: FEATURE: Añadir página de "/admin/settings"
  - [x] TODO: Modificar los links del sidebar de navegación de mobile y desktop para quitar el link a la página "/ajustes" y añadir nuevo enlace a la página "/admin/settings"
  - [x] TODO: Crear las siguientes pestañas en la página "/admin/settings":
    - [x] Pestaña "Empresa" a la que moveremos la página "/admin/company" en la nueva ruta "/admin/settings/company"
    - [x] Pestaña "Localizaciones" a la que moveremos la página "/admin/locations" en la nueva ruta "/admin/settings/locations",
    - [x] Pestaña "Equipos" a la que moveremos la página "/admin/departments" en la nueva ruta "/admin/settings/departments"
    - [x] Mover también la rutas "/admin/locations/[locationsId]" a la nueva ruta "/admin/settings/locations/[locationsId]"
    - [x] Mover también la ruta "/admin/departments/[departmentsId]" a la nueva ruta "/admin/settings/departments/[departmentsId]"
    - [x] Crear nueva pestaña con la página "Horarios" en la ruta "/admin/settings/horarios" vacía por el momento
    - [x] Crear nueva pestaña con la página "Calendarios" en la ruta "/admin/settings/calendarios" vacía por el momento

## 20250308

- [x] todo-00009.md

  - [x] Implement the "Calendarios" tab in the settings area with a nested vertical tab menu for "Calendarios Festivos" and "Calendarios Laborales"

- [x] todo-00010.md

  - [x] Implement the "Calendarios" tab in the settings area with a nested vertical tab menu for "Calendarios Festivos" and "Calendarios Laborales"
  - [x] Implement the "Calendarios Laborales" functionality with data model, logic, and UI

- [x] Test the CSV import functionality

- [x] todo-00011.md

  - [x] NEW FEATURE: "Calendarios Festivos". The purpose of this section will be to allow the user to add as many "holidays calendars" as he needs to use for a given localization or office for a given year. As you can see in the image, in this page the adminsitrator will be able to:
  - [x] UI: "Calendarios Festivos". Mejoras de UI/UX de la página de "Calendarios Festivos" y "Calendarios Laborales"

## 20250309

- [x] UI: "Calendarios Festivos". Mejoras de UI/UX de la página de "Calendarios Festivos" no mostrar sección de información general y mostrar fecha de creación en el título de la sección.
- [x] BUG FIX: corregir error en la página de "/admin/settings/calendarios/festivos" que cualquier sub-tab que seleccione la pestaña de navegación de la página de settings, se muestra el tab de "/empresa" como el tab activo.

- [x] Tested the functionality with real data, especially in the following scenarios:
- [x] Add validation and error handling
- [x] BUG FIX: depurar errores del linter y del builder `npm run build`

## Current focus

- [ ] 💥 TODO: Corregir errores de Linting y Building para subir a Vercel

- [ ] todo-00010.md

  - [x] NEW FEATURE: Añadir página de "/admin/settings"
  - [ ] NEW FEATURE: Añadir lógica, modelo y UI para definir y utilizar Horarios Normal y Reducido en el cálculo de computo de horas de los usuarios.

OPCIÓN: UTILIZAR UN VALOR DE HORAS DEFINIDO PARA CADA DÍA DE LA SEMANA

- [ ] TODO: FEATURE: Añadir lógica, modelo y UI para definir y utilizar Horarios Normal y Reducido en el cálculo de computo de horas de los usuarios.

- [ ] 1. TODO: FEATURE: Modificar la página "/admin/settings/horarios" para permitir añadir un botón como en la imagen que permita definir un horario que definirá el número de horas de trabajo para cada día de la semana.

  - [ ] Existirán dos tipos de horarios laborales en los que se establecerá una cantidad de horas a realizar para cada día de la semana:

    - [ ] 1. Horario Normal: se aplica para el cálculo de computo de horas trabajadas durante todo el año excepto en el periodo de "horario reducido"

      - [ ] El administrador deberá definir el número de horas estándar de trabajo para cada día de una semana que aplicará para este calendario
      - [ ] El administrador deberá definir los días de la fecha inicio y fecha fin de este horario

    - [ ] 2. Horario Reducido: se aplica para el cálculo de computo de horas trabajadas durante un periodo definido por el administrador

      - [ ] El administrador deberá definir el número de horas de trabajo para cada día de una semana que aplicará para este calendario
      - [ ] El administrador deberá definir los días de la fecha inicio y fecha fin de este horario

    - [ ] Por ejemplo: los tres intervalos de tiempo deberán cubrir todo el año y cada uno de ellos aplicará un horario normal o reducido diferente:
      - [ ] 1 enero 2025 - 30 junio 2025 Horario Normal: 40 horas semanales
      - [ ] 1 julio 2025 - 31 agosto 2025 Horario Normal: 37 horas semanales
      - [ ] 1 septiembre 2025 - 31 diciembre 2025 Horario Normal: 40 horas semanales

  - [ ] Cada día puede tener un número de horas estándar de trabajo diferente: los valores deben estar entre 0 y 8 horas.
  - [ ] Estos valores se aplicarán para el cálculo de las horas objetivo semanales de todos los empleados.

- [ ] 2. TODO: FEATURE: La página tendrá junto a cada tipo de horario, un valor con el sumatorio del número de horas definido para cada día de la semana: "Total horas objetivo semanales para Horario Normal" y "Total horas objetivo semanales para Horario Reducido""

LÓGICA DE CÁLCULO:

- [ ] 3. TODO: FEATURE: Modificar la lógica de cálculo de las páginas "/admin/computo-horas" y "/computo-horas".

CÁLCULO OBJETIVO HORAS SEMANALES:

- [ ] Se creará una lógica de servidor para calcular el valor objetivo de horas semanales para cada semana concreta teniendo en cuenta el tipo de calendario que aplica para cada día de la semana de esa semana concreta.

- [ ] Esta lógica tendrá en cuenta que:

  - [ ] deberá saber para un día del año concreto el calendario que aplica en ese día puede ser normal, o reducido
  - [ ] en función del día que se esté calculando se tendrá un valor u otro de horas objetivo semanales para ese día concreto:
    - [ ] Si el día de la semana para la fecha que se está calculando está dentro del periodo definido para el "horario reducido", se aplicará el valor definido para el día de la semana concreto (horas para lunes, o martes, o miércoles, o viernes) en el "horario reducido".
    - [ ] Para días que estén fuera del periodo definido para el "horario reducido" se aplicarán los valores de horas de trabajo definidos los días de la semana concretos (horas para lunes, o martes, o miércoles, o viernes) en el "horario normal".

- [ ] Se añadirá una columna "Objetivo Semana" en la tabla de las páginas "/admin/computo-horas" y "/computo-horas" para cada semana. Esta columna mostrará el valor objetivo de horas semanales calculado para todos los días de la semana concreta

CÁLCULO DIFERENCIAS HORAS TRABAJADAS Y OBJETIVO HORAS SEMANALES:

- [ ] Se creará la lógica de servidor para el cálculo de diferencias de horas trabajadas "Total" y de horas semanales "Objetivo Semana" para cada semana concreta.
- [ ] Modificar el valor de la columna "Diferencia" de las páginas "/admin/computo-horas" y "/computo-horas" para que ahora muestre el valor calculado de la diferencia entre el valor de la columna "Total" con el computo de horas registradas como horas trabajadas por el usaurio, y la columna "Objetivo horas".

CÁLCULO DE BOLSA DE HORAS:

- [ ] Se añadirá a las páginas "/admin/computo-horas" y "/computo-horas" una estadística calculada de "Bolsa de horas" que representará las horas de más, o de menos realizadas por un empleado.
- [ ] Será calculado como el total de las sumas de diferencias de todas las semanas del año seleccionado. Esta estadística estará colocada a la derecha del filtro del año.

MODELO DE DATOS:

- [ ] Crear modelo de datos para los horarios normales y reducidos
  - [ ] Deberá tener:
    - [ ] id_horario
    - [ ] tipo_horario: "normal" o "reducido"
    - [ ] nombre_horario
    - [ ] fecha_inicio
    - [ ] fecha_fin
    - [ ] total_horas_semanales: valor con el sumatorio de todos los valores de la propiedad "horas_semanales"
    - [ ] horas_diarias: array de 7 valores, uno para cada día de la semana distinto (lunes, martes, miércoles, jueves, viernes, sábado, domingo)

---

OPCIÓN A: UTILIZAR UN VALOR DE HORAS TOTALES DEFINIDO PARA LA SEMANA

- [ ] TODO: FEATURE: Añadir opción para definir el número de horas estándar de trabajo semanales según un rango de fechas concreto, definiendo dos tipos de calendarios:

  - [ ] Horario Normal: se aplica para el cálculo de computo de horas trabajadas durante todo el año excepto en el periodo de "horario reducido"

    - [ ] El administrador deberá definir el número de horas estándar de trabajo para una semana que aplica para este calendario

  - [ ] Horario Reducido: se aplica para el cálculo de computo de horas trabajadas durante un periodo definido por el administrador

    - [ ] El administrador deberá definir el número de horas estándar de trabajo para una semana que aplica para este calendario
    - [ ] El administrador deberá definir la fecha inicio y fecha fin de este horario

  - [ ] la lógica de cálculo de horas trabajadas semanales deberá tener en cuenta el valor de horas de la semana que debe realizar un empleado en función del calendario que aplica para la semana concreta, en función del periodo de tiempo que aplica el calendario reducido o normal, de forma que:

    - [ ] Para una un día de una semana concreta se determinará si la semana pertenece al calendario normal, o al calendario reducido.
    - [ ] En ambos casos, se aplicará el valor de horas estándar de trabajo correspondiente a un día de la semana definido para cada tipo de calendario (horas semanales definidas en el calendario a aplicar, divididas por 5 días laborables).

  - [ ] Se añadirá una columna en la tabla de las páginas "/admin/computo-horas" y "/computo-horas" para cada semana. Utilizará este valor de objetivo de horas semanales para calcular la diferencia con las horas trabajadas semanales y saber la diferencia con las horas trabajadas realmente.
  - [ ] las páginas "/admin/computo-horas" y "/computo-horas" tendrán un valor calculado de "computo de horas" con el total de las sumas de diferencias de todas las semanas del año seleccionado. Esta estadística estará colocada a la derecha del filtro del año.

---

- [ ] todo-00007.md

  - [ ] TODO: FEATURE: Presencia de equipo

### CALENDARIOS

- [x] Registro de Festivos

  - [x] Create admin feature to import and manage local and national holidays calendars ⚠️⚠️⚠️
    - Carga anual de los días festivos de Santa Cruz de Tenerife. Es igual para todos los trabajadores.
    - Reservado al role admin.

- [ ] Registro de Vacaciones
