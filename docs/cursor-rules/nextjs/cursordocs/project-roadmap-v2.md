# Project Roadmap (v0.2.0)

## REQUIRED FEATURES:

### INCIDENCIAS

- [x] TODO: FEATURE: Algoritmo de cálculo de incidencias

  - Los registros de entrada de tiempo (time-entries) cancelados no computan
  - Deben haber periodos de comienzo (start) y terminado (end) del mismo tipo durante el mismo día
  - Los conceptos son: Work, Training, Pause, Break, lunch, medical, etc.

  - Ejemplos:

    missing end work time

    - Start 10:00 - End 12:00 (Work)
    - Start 12:00 - End 14:00 (Lunch)
    - Start 14:00 - (Work)

    missing start work time

    -             - End 16:00 (Work)
    - Start 12:00 - End 12:30 (Lunch)
    - Start 17:00 - End 18:00 (Training)

### AUSENCIAS

- [x] TODO: FEATURE: Añadir un campo de comentario a la evaluación de ausencias.

### LOGGING SEGURO

- [ ] TODO: FEATURE: Fiable, inmodificable y no manipulable a posteriori. Para dar cobertura legal al registro ??? Crear una cadena md5 que relacione cada registro con el anterior y comunicarla al trabajador con cada fichaje registrado:

  - [ ] fichaje1.sello = md5(fichaje1.fechahora & fichaje1.otrosdatos)
  - [ ] fichajeN.sello = md5(fichajeN-1.sello & fichajeN.fechahora & fichajeN.otrosdatos)

### CALCULO SEMANAL, EXCESO DE HORAS, FESTIVOS, VACACIONES, BAJAS Y AUSENCIAS JUSTIFICADAS

- [ ] TODO: FEATURE: Cálculo del cómputo semanal de fichaje - El cómputo semanal se realizará sumando los valores diarios de lunes a viernes. En este caso el promedio semanal debería encontarse entre 37,5h y 40h.

  - Excepciones:
    - Valor inferior en Bajas, festivos y vacaciones.
    - Valor superior en autorización de horas extras.
  - El mes de agosto tiene jornada reducida, por lo que cada día del mes de agosto tendrá 0,5h de ausencia justificada asociado a la Jornada Reducida.
  - Se mostrará en “verde” o correcto el fichaje en la franja designada y en “rojo” el que se encuentra fuera de ella, asociado a la semana.
  - En el caso de que el trabajador sea reincidente en que supere las 40h semanales durante más de dos semanas consecutivas, se mostrará el aviso: “Para realizar horas extraordinarias es necesaria autorización. Las horas deben compensarse entre días.
  - El role admin podrá visualizar el cálculo de horas de todos los trabajadores.

- [ ] FEATURE: Exceso de horas: Necesitamos crear la lígica para representar el número de horas en exceso que tiene acumulado un usuario durante el año. Para ello vamos a calcular la diferencia de horas imputadas como tiempo trabajado (conceptos work y training) y las horas que debería trabajar en base al número de días laborales.

  - Para ello debemos definir un calendario de días de trabajo de lunes a viernes de 8 horas diarias de trabajo.
  - Por ahora no se consideran los días festivos
    - El algoritmo de exceso de horas debe tener en cuenta los días festivos.
    - El algoritmo de días con ausencias debe tener en cuenta los días festivos.

### CALENDARIOS

- [ ] Registro de Festivos

  - [ ] Create admin feature to import and manage local and national holidays calendars ⚠️⚠️⚠️
    - Carga anual de los días festivos de Santa Cruz de Tenerife. Es igual para todos los trabajadores.
    - Reservado al role admin.

- [ ] Registro de Vacaciones

  - [ ] Registro los días de vacaciones anuales. Serán 23 días laborables anuales por trabajador. En el
        caso de que el trabajador se haya incorporado ya comenzado el año, le corresponderá la parte
        proporcional.
  - [ ] Se registrará un día de vacaciones por jornada laborable. Los días de vacaciones deben indicar
        el año al que corresponden, pues es una práctica habitual disfrutar en enero vacaciones
        devengadas en el año anterior.
        Reservado al role admin.

- [ ] Registro de Bajas y ausencias justificadas

  - [ ] Las bajas y ausencias justificadas se registrarán como Ausencia Justificada, que serán 8 horas
        por cada jornada completa o un número determinado de horas inferior a 8 si se trata de una
        ausencia inferior a un día. Por ejemplo la asistencia a exámenes oficiales.

- [ ] Visualización del calendario laboral

  - [ ] Visualización de los días festivos en formato calendario. Igual para todos los trabajadores.

- [ ] Visualización de vacaciones

  - [ ] Visualización de las vacaciones del trabajador (individual) en formato calendario.
  - [ ] Visualización del calendario de vacaciones de toda la empresa.

- [ ] Create admin dashboard to display and manage Teams' Workdays

## ARQUITECTURA:

### ONBOARDING DE USUARIOS NO ADMIN:

- [ ] TODO: FEATURE: Proceso de invitación de usuarios no-admin (employees, managers)

  - [ ] TODO: FEATURE: crear formulario de invitación de usuarios no-admin (employees, managers):

    - nombre y apellidos
    - email
    - departamento
    - localización
    - role (employee, manager, admin)
    - time-zone
    - status = "pending"

  - [ ] TODO: FEATURE: enviar correo de invitación
  - [ ] TODO: FEATURE: Modificar los webhooks de API CLERK (api/webhooks/clerk) para comprobar si el usuario existe en la base de datos:
    - si existe, activarlo: quitar estado "pending" (pendiente) y ponerlo como "active" (activo)
    - si no existe, crearlo y enviarle un correo de bienvenida

### ONBOARDING DE USUARIOS ADMIN - SAAS:

- [ ] TODO: FEATURE: SAAS - Onboarding de usuarios admin al hacer signup para comprar el servicio. Utilizar STRIPE para la compra del servicio.

  - [ ] TODO: FEATURE: Crear un formulario de registro de usuario admin en el que se cree el nombre de la empresa y el slug antes de hacer signup y después de hacer la compra en stripe. DEFINIR ???

## FUNCIONALIDAD DE USUARIOS:

### NUEVA FEATURE: USERS/PRESENCIA-EQUIPO !!!

**20250222**

- [ ] TODO: FEATURE: Añadir página mi localización / mi equipo... facilitar a los USUARIOS el ver quienes trabajan en la empresa, departamento y equipo. Regla de negocio: todo el mundo puede ver a todo el mundo. Organization and team presence (who is working and who is not right now)

### MEJORAS FUNCIONALIDAD "/REGISTROS":

- [ ] TODO FEATURE: añadir opciones preconfiguradas para el filtro de fechas: hoy, esta semana, semana pasada, este mes, mes pasado, este año.

### MEJORAS FUNCIONALIDAD "/INDICENCIAS":

- [ ] TODO: FEATURE: Añadir opción a "/incidencias" para poder VISUALIZAR el día completo, no sólo el registro de con la incidencia
- [ ] TODO: FEATURE: añadir paginación a los "días incompletos" (Not implemented yet)
- [ ] TODO: FEATURE: diseñar bien la funcionalidad de las "incidencias". Qué queremos mostrar en la pantalla de "incidencias"? 1 mes, 3 meses, 6 meses, 1 año? todo ?

- [ ] TODO: FEATURE: añadir paginación a las "incidencias" (Not implemented yet)

## FUNCIONALIDAD DE ADMIN:

### MEJORAS FUNCIONALIDAD "ADMIN/USERS/REGITROS":

- [x] TODO: FEATURE: Ampliar el filtro de la página "/admin/users/registros" para permitir filtrar por usuario, además de los filtros actuales. El text field debe tener un debounce.
- [x] TODO: FEATURE: Añadir posibilidad de descarga de CSV de descarga de /registros & /admin/users/registros... lo filtrado.

- [x] TODO: FEATURE: Añadir opción a /registros para poder CREAR un "registro de entrada con detalles"

- [ ] TODO: FEATURE: Añadir funcionalidad de Managers para que pueda ver todos los registros de tiempo de todos los usuarios de su departamento.

  - [ ] TODO: FEATURE: Un usuario admin puede asignar un manager a un departamento desde la página de /admin/users/ o desde /admin/departments/departmentId mediante una acción.
  - [ ] TODO: FEATURE: Un usuario manager puede cancelar un registro de tiempo de cualquier usuario de su departamento.

### MEJORAS FUNCIONALIDAD "ADMIN/USERS/AUSENCIAS":

- [ ] TODO: FEATURE: managers should be able to see the AUSENCES of their team members

### ADMIN/DEPARTMENTS & ADMIN/LOCATIONS:

- [ ] TODO: FEATURE: Añadir opción en departamentos y localizaciones opción de poder llevar a la página de /admin/users/registros ya filtrando por ruta para ver lo de cada uno. Permitir también la página de /registros & /admin/uesrs/registros poder filtrar por departamento & localización
- [ ] TODO: FEATURE: Añadir opción en localizaciones para poder asignar una zona horaria a cada localización.

### ADMIN/COMPANY:

- [ ] Design and implement branding section
- [ ] Add logo upload functionality
- [ ] Implement company color scheme settings
- [ ] Add company-wide settings section

### ADMIN/LOCATIONS:

- [ ] Identify full address data from the map selection
- [ ] Address validation for data integrity

### APP SETTINGS:

- [ ] Create app settings and user preferences

### MEJORAS UI:

- [x] Añadir spinner o loading app.. en lugar de "Loading maps..."
- [x] Añadir Favicon correctamente a la app
- [x] Añadir "/admin/users/registros" página de "/admin" con enlaces a las herramientas con cards

- [ ] Añadir spinner a botones que trabajen con la BD de crear, editar, eliminar

  - "/jornada", "/registros", "/incidencias"
  - "/admin/\*"

### CHANNELS: CHATBOT NOTIFICATIONS & COMMANDS

- [ ] ChatBot de Telegram: Bot que permite realizar los fichajes desde la aplicación de Telegram.
- [ ] Calcula la hora de entrada y envía un mensaje al usuario para fichar a la hora estimada de llegada, sólo en el caso de no ser festivo ni vacaciones.
- [ ] Permite fichar la hora de salida. Muestra las horas trabajadas en el día y la tendencia que debe seguir el trabajador para no sobrepasar las 40 horas semanales ni quedar por debajo de 37,5h.

## DEUDA TÉCNICA IMPORTANTE

- [ ] REFACTOR: Guardar en almacenamiento local cookies las opciones del sidebar y dark-theme para que se carguen desde inicio (sidebar collapsed/expanded) así con cada refresco no se debería perder que tenga la barra lateral abierta o cerrada, como estaba... siempre se muestra cerrada tras un refresco

- [ ] REFACTOR: Estudiar como susituir los "hard-refresh" para actualizar páginas completas en lugar de lo que queremos actualizar, que son secciones concretas (por ejemplo, al añadir un usuario/registro nuevo; o editar el nombre de un departamento). Tener en cuenta la fucnionalidad de NExtjs nueva de revalidatePath, revalidateTag

  - https://nextjs.org/docs/app/building-your-application/data-fetching/incremental-static-regeneration

    - On-demand revalidation with revalidatePath (https://nextjs.org/docs/app/building-your-application/data-fetching/incremental-static-regeneration#on-demand-revalidation-with-revalidatepath)

    - On-demand revalidation with revalidateTag (https://nextjs.org/docs/app/building-your-application/data-fetching/incremental-static-regeneration#on-demand-revalidation-with-revalidatetag)

## PENDING REFACTORS

- [ ] REFACTOR: Traducir todos los textos de la app al español

- [ ] REFACTOR: Absences & Uncompleted Days:

  - [ ] Refactorizar el código para que se pueda calcular el número de días de ausencia y de días incompletos:
    - [ ] 1. para cada usuario en función de un valor de días de ausencia y de días incompletos por configuración de usuario para que se aplique por defecto. Se podrá elegir entre un periodo de tiempo (365 días, 180 días, 90 días, 60 días, 30 días, 15 días, 7 días, 1 día).
    - [ ] 2. se podrá elegir qué días se tienen en cuenta para calcular los días de ausencia y de días incompletos. Por ejemplo, se podría elegir que solo se tengan en cuenta los días laborables, los días laborables y los festivos, etc. Elegir lunes, martes, etc.
  - [ ] Paginar los resultados para que se pueda mostrar en la pantalla de "Incidencias" y en la pantalla de "Días incompletos".
  - [ ] Mejorar la UI de días incompletos para utilizar mejor el espacio en desktop

- [ ] 5. Testing & Optimization - Test with different location formats - Test error cases (no location, invalid coordinates) - Ensure mobile responsiveness - Optimize map loading performance

- [ ] Añadir a la página de "/pending" que se muestra cuando el usuario está pendiente de ser aprovado por el administrador, una comprobación previa para contemplar el caso de que el usuario tenga permisos de admin (al ser el primer usuario de una organización) y que viaje a "/", si no, que se quede en "/pending"

- [ ]

## BUGS

- [ ] BUG: cuando se hace un reset del filtro de la página de "/registros", no se resetean los filtros a sus valores por defecto (all).
- [ ] BUGFIX: refactor sidebar to better handle state management across all pages about when it's open and when it's collapsed, since when i navigate to some pages it automatically collapses (as expected in the previous design pattern)

- [ ] REFACTOR UI: Añadir logo de empresa en la cabecera del sidebar

- [ ] BUGFIX: cuando no se tiene una localización porque el sistema no pudo registrarla (probablemente porque el usuario no dio permisos para obtenerla) el mapa no muestra la localización de un registro en /registros. Muestra el mapa en blanco. El mapa funciona correctamente cuando se tiene una localización.

- [ ] BUG: parece que hay algún problema que hace que cuando vamos a hacer un registro, tarda unos segundos de más .... pero al final parece que lo crea... no sé si es de vercel, de neon FREE TIERS... o si es de la app...

- [ ] REFACTOR: Refactor to solve build errors: https://chatgpt.com/c/67b1fa1b-4a90-800e-a29b-2cc09c084037

  - [ ] Deprecation Warning (punycode - Analysis in document Punycode_module_deprecation_warning_analysis.md)
  - [ ] RevalidatePath Warning

    - [ ] Add "page" or "layout" as the second argument to revalidatePath. Modify your revalidatePath calls to include the correct type:

    ```typescript
    // ✅ Correct usage
    import { revalidatePath } from "next/cache"

    revalidatePath("/admin/departments/[id]", "page") // or "layout"

    // Choose the correct type:
    // "page" → If you want to revalidate only the page component.
    // "layout" → If you need to revalidate the entire layout.
    ```

### BUGS STILL NOT SOLVED:

- [ ] Arreglar el problema de Aria-Hidden en el sidebar (ver solución chatgpt con inert en mobile-nav.tsx https://chatgpt.com/c/67a4f2ed-76ec-800e-8cb3-597b5f191e8b)
- [ ] Arreglar el layout del formulario de registro de eventos en /dashboard que no me deja poner un padding en el DialogContent en mobile

- [ ] BUG: Arreglar el problema que tenemos después de añadir los mapas de Google Maps en el componente `MapModal.tsx`

```
As of February 21st, 2024, google.maps.Marker is deprecated. Please use google.maps.marker.AdvancedMarkerElement instead. At this time, google.maps.Marker is not scheduled to be discontinued, but google.maps.marker.AdvancedMarkerElement is recommended over google.maps.Marker. While google.maps.Marker will continue to receive bug fixes for any major regressions, existing bugs in google.maps.Marker will not be addressed. At least 12 months notice will be given before support is discontinued. Please see https://developers.google.com/maps/deprecations for additional details and https://developers.google.com/maps/documentation/javascript/advanced-markers/migration for the migration guide.
```
