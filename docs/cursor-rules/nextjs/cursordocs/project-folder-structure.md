# Folder Structure

```bash
❯ tree src  -L 9 -I "nodes_modules"
src
├── app
│   ├── (app)
│   │   ├── (admin)
│   │   │   └── admin
│   │   │       ├── company
│   │   │       │   ├── components
│   │   │       │   │   └── company-profile-form.tsx
│   │   │       │   └── page.tsx
│   │   │       ├── computo-horas
│   │   │       │   ├── components
│   │   │       │   │   ├── admin-weekly-hours-filter.tsx
│   │   │       │   │   ├── collapsible-filters.tsx
│   │   │       │   │   └── weekly-hours-table.tsx
│   │   │       │   └── page.tsx
│   │   │       ├── layout.tsx
│   │   │       ├── page.tsx
│   │   │       ├── settings
│   │   │       │   ├── calendarios
│   │   │       │   │   ├── calendarios-tabs.tsx
│   │   │       │   │   ├── festivos
│   │   │       │   │   │   ├── [id]
│   │   │       │   │   │   │   ├── associate-labor-calendar-button.tsx
│   │   │       │   │   │   │   ├── calendar-view.tsx
│   │   │       │   │   │   │   ├── holiday-calendar-details.tsx
│   │   │       │   │   │   │   └── page.tsx
│   │   │       │   │   │   ├── create-holiday-calendar-button.tsx
│   │   │       │   │   │   ├── holiday-calendar-list.tsx
│   │   │       │   │   │   └── page.tsx
│   │   │       │   │   ├── laborales
│   │   │       │   │   │   ├── [id]
│   │   │       │   │   │   │   ├── add-holiday-date-button.tsx
│   │   │       │   │   │   │   ├── edit-holiday-date-button.tsx
│   │   │       │   │   │   │   ├── holiday-date-actions.tsx
│   │   │       │   │   │   │   ├── import-csv-button.tsx
│   │   │       │   │   │   │   └── page.tsx
│   │   │       │   │   │   ├── calendar-list.tsx
│   │   │       │   │   │   ├── create-calendar-button.tsx
│   │   │       │   │   │   ├── edit-calendar-button.tsx
│   │   │       │   │   │   └── page.tsx
│   │   │       │   │   ├── layout.tsx
│   │   │       │   │   └── page.tsx
│   │   │       │   ├── company
│   │   │       │   │   ├── components
│   │   │       │   │   │   └── company-profile-form.tsx
│   │   │       │   │   └── page.tsx
│   │   │       │   ├── departments
│   │   │       │   │   ├── [departmentId]
│   │   │       │   │   │   ├── components
│   │   │       │   │   │   │   ├── add-member-dialog.tsx
│   │   │       │   │   │   │   ├── department-header.tsx
│   │   │       │   │   │   │   ├── department-members-table.tsx
│   │   │       │   │   │   │   └── remove-member-dialog.tsx
│   │   │       │   │   │   ├── error.tsx
│   │   │       │   │   │   ├── hooks
│   │   │       │   │   │   │   ├── use-available-users.ts
│   │   │       │   │   │   │   ├── use-department-members.ts
│   │   │       │   │   │   │   └── use-organization.ts
│   │   │       │   │   │   └── page.tsx
│   │   │       │   │   ├── components
│   │   │       │   │   │   ├── columns.tsx
│   │   │       │   │   │   ├── department-actions.tsx
│   │   │       │   │   │   ├── department-dialog.tsx
│   │   │       │   │   │   ├── department-form.tsx
│   │   │       │   │   │   ├── department-members-table.tsx
│   │   │       │   │   │   ├── department-schema.ts
│   │   │       │   │   │   ├── departments-table.tsx
│   │   │       │   │   │   └── departments-wrapper.tsx
│   │   │       │   │   └── page.tsx
│   │   │       │   ├── horarios
│   │   │       │   │   └── page.tsx
│   │   │       │   ├── layout.tsx
│   │   │       │   ├── locations
│   │   │       │   │   ├── [locationId]
│   │   │       │   │   │   ├── components
│   │   │       │   │   │   │   ├── add-member-dialog.tsx
│   │   │       │   │   │   │   ├── location-header.tsx
│   │   │       │   │   │   │   ├── location-members-table.tsx
│   │   │       │   │   │   │   └── remove-member-dialog.tsx
│   │   │       │   │   │   ├── error.tsx
│   │   │       │   │   │   ├── hooks
│   │   │       │   │   │   │   └── use-available-users.ts
│   │   │       │   │   │   └── page.tsx
│   │   │       │   │   ├── components
│   │   │       │   │   │   ├── data-table-column-header.tsx
│   │   │       │   │   │   ├── data-table.tsx
│   │   │       │   │   │   ├── location-actions.tsx
│   │   │       │   │   │   ├── location-cell.tsx
│   │   │       │   │   │   ├── location-dialog.tsx
│   │   │       │   │   │   ├── location-form.tsx
│   │   │       │   │   │   ├── location-schema.ts
│   │   │       │   │   │   └── locations-table.tsx
│   │   │       │   │   └── page.tsx
│   │   │       │   ├── page.tsx
│   │   │       │   └── settings-tabs.tsx
│   │   │       └── users
│   │   │           ├── page.tsx
│   │   │           └── registros
│   │   │               ├── components
│   │   │               │   ├── admin-time-entries-filter.tsx
│   │   │               │   ├── admin-time-entries-table.tsx
│   │   │               │   ├── collapsible-filters.tsx
│   │   │               │   └── export-csv-button.tsx
│   │   │               └── page.tsx
│   │   ├── (users)
│   │   │   ├── computo-horas
│   │   │   │   ├── components
│   │   │   │   │   ├── collapsible-filters.tsx
│   │   │   │   │   ├── weekly-hours-filter.tsx
│   │   │   │   │   └── weekly-hours-table.tsx
│   │   │   │   └── page.tsx
│   │   │   ├── incidencias
│   │   │   │   ├── components
│   │   │   │   │   ├── recent-absences-list.tsx
│   │   │   │   │   ├── recent-absences-section.tsx
│   │   │   │   │   ├── time-entry-dialog.tsx
│   │   │   │   │   ├── uncompleted-days-list.tsx
│   │   │   │   │   └── uncompleted-days-section.tsx
│   │   │   │   └── page.tsx
│   │   │   ├── jornada
│   │   │   │   ├── components
│   │   │   │   │   ├── current-day.tsx
│   │   │   │   │   ├── dashboard-header.tsx
│   │   │   │   │   ├── event-registration-control-panel.tsx
│   │   │   │   │   ├── event-registration-form.tsx
│   │   │   │   │   ├── incidences-stats.tsx
│   │   │   │   │   ├── pending-days-alert.tsx
│   │   │   │   │   ├── pending-days-dialog.tsx
│   │   │   │   │   ├── worked-hours-chart.tsx
│   │   │   │   │   └── worked-hours.tsx
│   │   │   │   └── page.tsx
│   │   │   ├── layout.tsx
│   │   │   └── registros
│   │   │       ├── components
│   │   │       │   ├── collapsible-filters.tsx
│   │   │       │   ├── register-time-entry-button.tsx
│   │   │       │   ├── time-entries-filter.tsx
│   │   │       │   └── time-entries-table.tsx
│   │   │       └── page.tsx
│   │   ├── error.tsx
│   │   ├── layout.tsx
│   │   └── not-found.tsx
│   ├── (marketing)
│   │   ├── (auth)
│   │   │   ├── layout.tsx
│   │   │   ├── pending
│   │   │   │   └── page.tsx
│   │   │   ├── sign-in
│   │   │   │   └── [[...sign-in]]
│   │   │   │       └── page.tsx
│   │   │   ├── sign-out
│   │   │   │   └── [[...sign-out]]
│   │   │   │       └── page.tsx
│   │   │   ├── sign-up
│   │   │   │   └── [[...sign-up]]
│   │   │   │       └── page.tsx
│   │   │   ├── test-auth
│   │   │   │   └── [[...rest]]
│   │   │   │       └── page.tsx
│   │   │   ├── test-user
│   │   │   │   └── page.tsx
│   │   │   └── unauthorized
│   │   │       └── page.tsx
│   │   ├── about
│   │   │   └── page.tsx
│   │   ├── components
│   │   │   ├── cta.tsx
│   │   │   ├── features.tsx
│   │   │   ├── footer.tsx
│   │   │   ├── hero.tsx
│   │   │   ├── mobile-nav.tsx
│   │   │   ├── mouse-move-effect.tsx
│   │   │   ├── navbar.tsx
│   │   │   ├── redirect-to-jornada.tsx
│   │   │   ├── scroll-link.tsx
│   │   │   └── theme-toggle.tsx
│   │   ├── error.tsx
│   │   ├── features
│   │   │   └── page.tsx
│   │   ├── layout.tsx
│   │   ├── not-found.tsx
│   │   ├── nueva-ley-control-horario
│   │   │   ├── components
│   │   │   │   └── benefits.tsx
│   │   │   └── page.tsx
│   │   ├── page.tsx
│   │   └── precios
│   │       └── page.tsx
│   ├── actions
│   │   ├── actions.ts
│   │   ├── admin.ts
│   │   ├── calendar.ts
│   │   ├── departments.ts
│   │   ├── holiday-calendar.ts
│   │   ├── incidences.ts
│   │   ├── locations.ts
│   │   ├── organization.ts
│   │   ├── schemas
│   │   │   └── organization-schema.ts
│   │   ├── time-entries.ts
│   │   ├── users-time-entries-export.ts
│   │   ├── users.ts
│   │   ├── weekly-hours-admin.ts
│   │   └── weekly-hours.ts
│   ├── api
│   │   ├── user
│   │   │   └── role
│   │   │       └── route.ts
│   │   └── webhooks
│   │       └── route.ts
│   ├── error.tsx
│   ├── favicon.png
│   ├── globals.css
│   ├── layout.tsx
│   ├── not-found.tsx
│   └── providers.tsx
├── components
│   ├── avatar
│   │   ├── custom-avatar.tsx
│   │   └── user-avatar.tsx
│   ├── dialogs
│   │   ├── assign-department-dialog.tsx
│   │   ├── cancel-time-entry-dialog.tsx
│   │   └── view-cancellation-reason-dialog.tsx
│   ├── navigation
│   │   ├── mobile-nav.tsx
│   │   ├── sidebar.tsx
│   │   └── user-nav.tsx
│   ├── providers
│   │   └── google-maps-provider.tsx
│   ├── tables
│   │   ├── users-table-filters-client.tsx
│   │   ├── users-table-filters.tsx
│   │   └── users-table.tsx
│   ├── theme
│   │   ├── theme-provider.tsx
│   │   └── theme-toggle.tsx
│   └── ui
│       ├── alert-dialog.tsx
│       ├── alert.tsx
│       ├── avatar.tsx
│       ├── badge.tsx
│       ├── button.tsx
│       ├── calendar.tsx
│       ├── card.tsx
│       ├── chart.tsx
│       ├── checkbox.tsx
│       ├── dialog.tsx
│       ├── drawer.tsx
│       ├── dropdown-menu.tsx
│       ├── form.tsx
│       ├── input.tsx
│       ├── label.tsx
│       ├── location-map-modal.tsx
│       ├── map-modal.tsx
│       ├── pagination-numbers.tsx
│       ├── pagination.tsx
│       ├── popover.tsx
│       ├── radio-group.tsx
│       ├── select.tsx
│       ├── separator.tsx
│       ├── sheet.tsx
│       ├── switch.tsx
│       ├── table.tsx
│       ├── tabs.tsx
│       ├── textarea.tsx
│       ├── toast.tsx
│       ├── toaster.tsx
│       └── tooltip.tsx
├── db
│   ├── index.ts
│   ├── migrate-calendar-events.sql
│   ├── schema.ts
│   ├── seed.ts
│   ├── seed_create_15_users.ts
│   └── seed_users.ts
├── hooks
│   ├── use-debounce.ts
│   ├── use-toast.ts
│   ├── use-user-role.ts
│   └── use-window-size.ts
├── lib
│   ├── auth.ts
│   ├── server-action-handler.ts
│   ├── services
│   │   ├── time-calculation.service.ts
│   │   └── time-stats.service.ts
│   ├── time-entries-utils.ts
│   ├── utils.ts
│   └── validations
│       ├── calendar.ts
│       └── holiday-calendar.ts
├── middleware.ts
└── types
    ├── chart-date-range.ts
    ├── device-type.ts
    ├── index.ts
    ├── pending-day.ts
    ├── time-entry-concept.ts
    ├── time-entry-state.ts
    ├── time-entry.ts
    ├── time-entrytype-type.ts
    ├── uncompleted-day.ts
    ├── weekly-hours.ts
    ├── work-hours-data.ts
    └── worked-hour-data.ts

79 directories, 227 files
```
