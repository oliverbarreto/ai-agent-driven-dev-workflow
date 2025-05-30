# PROJECT ROADMAP (v0.1.0)

## Phase 1: Project Setup and Infrastructure

- [x] Initialize Nextjs 15 project structure with App router, Shadcn, Tailwind CSS
- [x] Create project on Vercel
- [x] Create project on Neon
- [x] Create project on Clerk
- [x] Initialize project on Vercel

## Phase 2: Basic Initialization

- [x] Initialize project to work with Drizzle ORM on Neon
- [x] Initialize project to work with Clerk
- [x] Create basic data models for the project
- [x] Create a basic time tracking system with clock-in and clock-out
- [x] Create logic to calculate the total time worked in a day
- [x] Create basic app structre for registering daily hours
- [x] Create graphs to display time worked in a day, week, month, year, etc.
- [x] Create basic app structre for registering displaying and filtering a registry of daily hours

## Phase 3: Refactor Functionality

- [x] Refactor model and logic of time tracking system with new requirements in prd_v2.md (cancelations, new fields in time_entries table, etc.)
- [x] Refactor time tracking system with clock-in and clock-out work time and break time
- [x] Refactor logic to calculate the total time worked in a day
- [x] Refactor pages and components to use the new model and logic of time tracking system
  - [x] Refactor page design for Event Registration Control Panel
  - [x] Refactor app structre for registering daily hours
  - [x] Revisar y Refactor graphs to display time worked in a day, week, month, year, etc.
  - [x] Revisar y Refactor de la app structre y de la página de tabla de registros de horas (/registros) para que se pueda filtrar por fecha y por tipo (start, end) y concepto de registro (trabajo, formación, almuerzo, médico, otro, etc.)
  - [x] Add functionality to add pagination to the time entries table (use tankstack for pagination)
- [x] Add new functionality to mark time entries as "cancelled"

  - [x] Hacer funcionalidad de cancelar un registro de horas (Analizar si hay que modificar el modelo de datos de la tabla time_entries con una columna "is_cancelled", en lugar de la tabla actual relacionada con las cancelaciones).
    - [x] RESULTADO: Mejor no tocar la tabla de "time_entry_cancellation" por ahora. Seguimos con la tabla relacionada con las cancelaciones.
  - [x] Analyze the current schema in which we have "time_entries" table and "time_entry_cancellation" table to create logic and actions to access the data required to provide the new feature.
  - [x] Add new functionality to allow the user to cancel "time-entries" from:

    - [x] 1. from the list of events registered for current date in the component "current-day.tsx" in the page "/jornada"
    - [x] 2. from the table with time entries with in the component "time-entries-table.tsx" in the page "/registros"

## Phase 4: New functinoality to create "Recent Absences" component.

- [x] Add new functinoality to create a new "Incidence List" component. It should display a list of all "absences" for the current user: that is days without any time entry at all; and "Uncompleted Days" which are dates with at least one unfinished session, work/training or any other type, lunch, medical, break, other, etc.

## Phase 5: Core USER Functionality

### Phase 5.1: Database Schema and Setup

- [x] Review and update database schema for:
  - [x] Companies table
  - [x] Teams table
  - [x] Users table with Clerk integration
  - [x] Relationships between tables

### Phase 5.2: Authentication Implementation

- [x] Initial Clerk Setup
  - [x] Create Clerk project with email and Google auth
  - [x] Add environment variables
  - [x] Setup middleware
  - [x] Add ClerkProvider to layout
- [x] Modify schema to:
  - [x] include clerk users info and roles
  - [x] include organization/company info
  - [x] include department/team info
  - [x] push schema changes to database
- [x] Enable basic user signup, loging and logout with Clerk
- [x] User Authentication Flow
  - [x] Add login/signup UI components to navigation
  - [x] Test Clerk authentication
  - [x] Implement protected routes
    - [x] Configure basic auth protection
    - [x] Add role-based protection
    - [x] Test protection flows
    - [x] Handle unauthorized access
  - [x] Modify logic to handle logged in user
  - [x] Add user role-based access control
  - [x] Create pending user approval flow

### Phase 5.3: Webhook Integration

- [x] Setup webhook infrastructure
  - [x] Install and configure Svix
  - [x] Setup Ngrok for local testing
- [x] Implement webhook endpoints
  - [x] User creation webhook
  - [x] User update webhook
  - [x] User deletion webhook

### Phase 5.4: Admin Dashboard to manage users

- [x] User Management
  - [x] Implement users CRUD operations
  - [x] Create users dashboard
  - [x] Implement user approval workflow
  - [x] Add role management functionality

### Phase 5.5: Core ADMIN Functionality

- [x] Create admin dashboard to display and manage users
- [x] Create admin dashboard to display and manage Teams
- [x] Company Management:

  - [x] Implement company CRUD operations
  - [x] Create company settings page

- [x] Locations/Centros de Trabajo Management:

  - [x] Implement locations CRUD operations
  - [x] Create locations dashboard

- [x] Department/Team Management:

  - [x] Implement team CRUD operations
  - [x] Create teams page with a table of teams and CRUD operations
  - [x] Implement team member management in team-members page

### Phase 5.6: Refactor functionality of current (admin) routes: /admin, /admin/company, /admin/locations, /admin/departments to work with current logged in user with Clerk

- [x] Refactor current functionality to work with current logged in user with Clerk
  - [x] 1. Refactor for routes: /admin, /admin/company, /admin/locations, /admin/departments

IMPORTANT NOTE:

1. Do not modify the functionality of the (admin) routes (/admin, /admin/company, /admin/locations, /admin/departments)
2. Do not modify the UI or design, just the functionality

### Phase 5.7: Refactor functionality of current (users) routes: /jornada, /incidencias, /registros to work with current logged in user with Clerk

- [x] Phase 5.7: Refactor functionality of current (users) routes: /jornada, /incidencias, /registros to work with current logged in user with Clerk

  - [x] 1. Refactor the app functionality for routes (/jornada, /incidencias, /registros) under the folder (users) to work with the current logged in user via Clerk authentication

    - [x] Modify the server actions to work with the current logged in user
    - [x] Modify the client components to work with the current logged in user
    - [x] Modify the server components to work with the current logged in user

  > IMPORTANT NOTE:
  >
  > 1. Do not modify the functionality of the (admin) routes (/admin, /admin/company, /admin/locations, /admin/departments)
  > 2. Do not modify the UI or design, just the functionality

### Phase 5.8: Test the functionality of the routes (/jornada, /incidencias, /registros) under the folder (users) to work with the current logged in user via Clerk authentication

- [ ] Test the functionality of the routes (/jornada, /incidencias, /registros) under the folder (users) to work with the current logged in user via Clerk authentication

  > IMPORTANT NOTE:
  >
  > 1. Do not modify the functionality of the (admin) routes (/admin, /admin/company, /admin/locations, /admin/departments)
  > 2. Do not modify the UI or design, just the functionality

NEXT STEPS:

- [ ] 1. Testing and Validation of (USERS) routes:

  - [x] ✅ BUGFIX: el botón de refresh debe resetear los filtros a sus valores por defecto, solo resetea el filtro de fecha
  - [ ] TODO: FEATURE: añadir opciones preconfiguradas para el filtro de fechas: hoy, esta semana, semana pasada, este mes, mes pasado, este año.
  - [x] ✅ BUGFIX: el nombre de usuario no se muestra en el listado de registros (Unknown)
  - [x] ✅ BUGFIX: revisar si se está almacenando bien la localización donde se hace el registro
  - [x] ✅ BUGFIX: se están calculando mal los días incompletos para el usuario actual
  - [ ] TODO: añadir paginación a los "días incompletos" (Not implemented yet)
  - [ ] TODO: diseñar bien la funcionalidad de las "incidencias". Qué queremos mostrar en la pantalla de "incidencias"? 1 mes, 3 meses, 6 meses, 1 año? todo ?
  - [ ] TODO: añadir paginación a las "incidencias" (Not implemented yet)

  - [x] Test all routes with unauthenticated users

    - [x] Users with employee role
    - [x] Users with admin role
    - [x] Users with manager role

  - [x] Test role-based access control and data isolation between organizations and users. The app is now only working with one organization, so we need to test if the data is isolated between users, within the same organization.

    - [x] Jornada page (/jornada):

      - [x] Event Registration Control Panel:

        - [x] Current time live update
        - [x] Weekly hours stats
        - [x] register time entries
          - [x] start/stop time entries
          - [x] register time entries with details for incidences:
            - [x] previous time entries
            - [x] future time entries
        - [x] cancel time entries
        - [x] Incidences Stats:
          - [x] Recent Absences number
          - [x] Uncompleted Days number in the last 60 days

      - [x] Today's Day:

        - [x] cancel time entries
        - [x] First start & last end entries stats
        - [x] Worked time stats
        - [x] Exceeded time threshold
        - [x] Refresh time button (clock icon)

      - [x] Worked hours graph

        - [x] this week
        - [x] last week
        - [x] this month
        - [x] last month
        - [x] this year
        - [x] Refresh stats button (refresh icon)

    - [x] Registros page (/registros):

      - [x] get time entries according to filters:
        - [x] date range
        - [x] time entry type
        - [x] time entry concept
        - [x] time entry status (is incidence or not)
        - [x] time entry is cancelled or not
      - [x] get paginated time entries
      - [x] actions: cancel time entries

    - [x] Incidencias page (/incidencias):

      - [x] Días Incompletos:
        - [x] Comprobar si se calcula bien los días incompletos: ERROR
      - [x] Incidencias:
        - [x] Comprobar si se calcula bien los incidencias: sí

  - [ ] Test data isolation between organizations

- [ ] 2. Testing and Validation of (ADMIN) routes:

  - [x] "/admin/users"
    - [ ] TODO: ❌ BUGFIX: managers cannot access "/admin/users" page, and they cannot assign users to departments
    - [ ] TODO: ❌ BUGFIX: no se puede acceder al modal que permite asignar un usuario a un departamento en /admin/users
    - [ ] TODO: ❌ FEATURE: falta añadir opción de eliminar usuario de departamento en /admin/users desde la tabla de usuarios
    - [ ] TODO: ❌ FEATURE: falta añadir paginación a la tabla de usuarios
  - [ ] "/admin/locations"
    - [ ] TODO: ❌ BUGFIX: hay que añadir un modal de confirmación para eliminar un departamento. Ahora no permite en el caso de que hayan usuarios asignado por constrains de las relaciones de las tablas.
  - [x] "/admin/departments"

    - [ ] TODO: ❌ BUGFIX: hay que añadir un modal de confirmación para eliminar un departamento. Ahora no permite en el caso de que hayan usuarios asignado por constrains de las relaciones de las tablas.

  - [x] Test all routes with authenticated users

  - [x] admin/users page:

    - [x] Tabla con usuarios
    - [x] Botón de acciones para cada usuario:
      - [x] Bloquear usuario
      - [x] Marcar como admin
      - [x] Marcar como manager
      - [x] Marcar como employee
      - [x] Eliminar usuario
      - [x] Asignar usuario a un departamento: ERROR
      - [x] Eliminar usuario de un departamento

  - [x] admin/company page:

    - [x] permite editar información en la BD

  - [x] admin/locations page:

    - [x] Permite añadir una localización
    - [x] Permite editar una localización
    - [x] Permite eliminar una localización
    - [x] Permite navegar a la página de usuarios de una localización: admin/locations/locationId
    - [x] admin/locations/locationId page:

      - [x] Permite añadir un usuario a una localización
      - [x] Permite eliminar un usuario de una localización

  - [x] admin/departments page:

    - [x] Permite añadir un departamento
    - [x] Permite editar un departamento
    - [x] Permite eliminar un departamento: ERROR
    - [x] Permite navegar a la página de usuarios de un departamento: admin/departments/departmentId
    - [x] admin/departments/departmentId page:

      - [x] Permite Añadir usuarios en departamento
      - [x] Permite eliminar usuarios de un departamento

## Phase 6 Bug fixing (users) & (admin) routes:

- [ ] 1. Testing and Validation of (USERS) routes:

  - [ ] "/registros"

    - [x] TODO: ✅ BUGFIX: el botón de refresh debe resetear los filtros a sus valores por defecto, solo resetea el filtro de fecha
    - [x] TODO: ✅ BUGFIX: el nombre de usuario no se muestra en el listado de registros (Unknown)
    - [x] TODO: ✅ BUGFIX: revisar si se está almacenando bien la localización donde se hace el registro
    - [ ] TODO FEATURE: añadir opciones preconfiguradas para el filtro de fechas: hoy, esta semana, semana pasada, este mes, mes pasado, este año.

  - [ ] "/incidencias"
    - [x] TODO: ✅ BUGFIX: se están calculando mal los días incompletos para el usuario actual
    - [ ] TODO FEATURE: añadir paginación a los "días incompletos" (Not implemented yet)
    - [ ] TODO FEATURE: diseñar bien la funcionalidad de las "incidencias". Qué queremos mostrar en la pantalla de "incidencias"? 1 mes, 3 meses, 6 meses, 1 año? todo ?
    - [ ] TODO FEATURE: añadir paginación a las "incidencias" (Not implemented yet)

- [x] 2. Testing and Validation of (ADMIN) routes:

  - [x] "/admin/users"

    - [x] TODO: ✅ BUGFIX: el formulario ahora funciona como se esperaba, pero hay un problema. Como puede ver en la imagen, tenemos un error de validación de restricción. No permite eliminar un usuario ya que el usuario tiene entradas en la tabla de entradas de tiempo en la base de datos. Sin embargo, el usuario administrador debería poder eliminar al usuario del sistema. Esto significa que debe estar seguro, de ahí el cuadro de diálogo de confirmación, para advertir que TODOS LOS REGISTROS asociados con el usuario también se eliminarán.

    AHORA ELIMINAR UN USUARIO SIGNIFICA "BLOQUEAR" al usuario.

    En este punto de la aplicación NO se va a eliminar el usuario, solo se va a bloquear. Hay que pensar qué funcionalidad se quiere tener para los registros:

    - Se elimina todo y nunca más se accede al usuario ni a sus registros del sistema. La empresa puede querer acceder al histórico de trabajo de un usuario ?
    - Se elimina el usuario per se, pero se mantiene el historial de registros ?

    - [x] TODO: ✅ BUGFIX: managers cannot access "/admin/users" page, and they cannot assign users to departments
    - [x] TODO: ✅ BUGFIX: no se puede acceder al modal que permite asignar un usuario a un departamento en /admin/users
    - [x] TODO: ✅ FEATURE: falta añadir opción de eliminar usuario de departamento en /admin/users desde la tabla de usuarios. Dejarlo sin departamento (es opcional). Ya está incluida en la opción de "Asignar usuario a un departamento", simplemente seleccionando "Sin departamento"
    - [ ] TODO FEATURE: falta añadir paginación a la tabla de usuarios

  - [x] "/admin/locations"

    - [x] TODO: ✅ BUGFIX: hay que añadir un modal de confirmación para eliminar un departamento. Ahora no permite en el caso de que hayan usuarios asignado por constrains de las relaciones de las tablas.

  - [x] "/admin/departments"
    - [x] TODO: ✅ BUGFIX: hay que añadir un modal de confirmación para eliminar un departamento. Ahora no permite en el caso de que hayan usuarios asignado por constrains de las relaciones de las tablas.

### Phase 6a: NEW FEATURES (admin) routes:

- [x] 1. (ADMIN) routes:

  - [x] "/admin/users"

    - [x] TODO: ✅ FEATURE: falta añadir paginación a la tabla de usuarios
    - [x] TODO: ✅ FEATURE: falta añadir opción de ordenación a las columnas de la tabla de usuarios
