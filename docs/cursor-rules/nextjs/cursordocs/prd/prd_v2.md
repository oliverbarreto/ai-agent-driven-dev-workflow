# New Features and Refactors:

# 5. Refactor: Time Entries Schema

Given the current schema with Neon DB and Drizzle in a NextJS 15 app, we need to make a refactoring because we need to incorporate new requirements on the data that we store and manage about time entries. These changes will allow new features to be implemented in the future.

## CURRENT SCHEMA:

@[paste code]

## CURRENT REQUIREMENTS:

### Workday Time Tracking

The application will have a real time clock-in/clock-out system that will be used to track the time of the users, allowing Employees to log their workday: clock-in time, clock-out time, training, lunch breaks, rest periods, and pauses, with the ability to add notes and images.

We have the following events:

- Start Session: start
- End Session: end

Work hours will be tracked as follows:

- Work Sessions: will be considered as working time
- Training Sessions: will be considered as working time
- Break Sessions: will be considered as break time (lunch break, rest period, other, medical leave, etc.)

The system will have a button to start a sesion, and a button to end a session. It will also have the options to select the type of session: work, training, break, lunch, medical leave, other, etc.

The system should register the device and location from which employees check in or out. This information will be stored in the database and will be displayed in when showing events of the user's time entries in the application.

### Use case for the time tracking

When interacting with the application:

- The employee must always end all sessions in the day, so the system can calculate the total time worked in the day.
- the employee can start a work session with a start event and type "work". An employee can have multiple work sessions in the day. However, the employee must always end a work session with an end event of type "work".
- The employee can start a work session with a start event and type "training". An employee can have as multiple training sessions in the day. The employee must always end a training session with an end event of type "training".
- The employee can start a break session with a start event and the type of break "lunch", "rest", "other", "medical leave", "other", etc. An employee can have as multiple break sessions in the day of various types. However, the employee must always end a break session with an end event of the same type. For example, if the employee starts a break session of type "lunch", he must always end it with an end event of type "lunch".

### Incidences:

- The employee might not be able to register the end of a session because he does not have internet connection or the application is not working, or any other reason. Therefore the system must allow the employee to register start or end events for any type for a given day and time in different day (later day). The employe can have multiple incidences in the day, or various incidences in different days.
- The system should identify incidences pending to be registered and warn the employee accordingly. It should provide date (day, month, year) and the expected event type (start or end) to be registered and the concept of the entry pending to be registered (lunch, rest, other, medical leave, other, etc.).

When interacting with the application:

- There will be a warning if the employee does not end one or more work sessions in the day.
- There will be a warning if the employee does not end one or more breaks in the day.
- The system must allow the employee to register events for a day and time in different day (later day) to end and fix incidences of periods of previous days. It might also be possible that the employee has an ending event having a start event pending to be registered.
- for example: the system must allow the case that an employee does not register a lunch break start, or the end of a workday, and the next day he can register both missing events: by creating entries for both start lunch break and end workday.

### UI:

- There will be buttons in the UI to allow the employee to directly register the start or end of a work session, meaning that the system will register an entry for type: start/end and concept: work.
- There will be another button to allow the employee to register more detailed time-entries.
  - This UI will allow the employee to register an event of any type and concept.
  - The dialog to enter detailed time-entries and to fix incidences of previous days, needs to allow to easily enter a date (day, month, year) and time (hour and minutes) and should create a valid time entry in the database, plus the rest of necessary data for the time-entry in the database.
  - This same UI will also allow registering an incidence of any type and concept for a previous date/hour than the current date/hour.
  - The logic of the use case behind this UI must check if the date/time is of a previous date/hour than the current date/hour. If so, it should then mark the entry as an incidence in the database and warn the employee that he is actually registering an incidence.
- The system should warn the user that there are pending events to register on the system.
- If the employee should have various days to fix, the system should list them. The Employee can use the UI to fix them one by one with the form.

## NEW REQUIREMENTS:

The new requirements are the following:

- We need to add new columns to the time-entries table to store the following new pieces of data for each time-entry:
  - Device: the device where the entry was registered (mobile, tablet, desktop)
  - Concept: concept associated to the entry (work, training, lunch, other)
  - Application: the name of the application associated to the entry: "Fichajes", or future apps that we will develop. The name will be stored as a text column.
  - Incidence: we must mark an entry as an incidence when the user registers an entry with a time of entry (timestamp) that is earlier than the current time, the incidence description will be stored using the current notes text column.

There is another new functional requirement, which is that users and admins can both delete a time-entry. But the system will never delete the record on the database. It should allow to mark it as "cancelled" and should keep additional info such as: concept of why it was cancelled (text), an cancellation_id, and the time-entry id that is associated with.

Take also into account that a user will have access to al his records on the time-entry table, and he would also need to have access to and see those that were cancelled and the details of those cancellations.

## NEW SCHEMA:

Here's the updated schema incorporating the new requirements while optimizing for enums where appropriate:

```typescript
import { pgTable, text, timestamp, pgEnum } from "drizzle-orm/pg-core"
import { createId } from "@paralleldrive/cuid2"
import { users } from "./users"

// Enums
export const timeEntryTypeEnum = pgEnum("time_entry_type", [
  "start",
  "end",
  "start_break",
  "end_break"
])

export const deviceEnum = pgEnum("device", ["mobile", "tablet", "desktop"])

export const conceptEnum = pgEnum("concept", [
  "work",
  "training",
  "break",
  "lunch",
  "other"
])

export const timeEntries = pgTable("time_entries", {
  id: text("id")
    .primaryKey()
    .$defaultFn(() => createId()),
  userId: text("user_id")
    .notNull()
    .references(() => users.id),
  type: timeEntryTypeEnum("type").notNull(), // Enforcing enum for consistency
  timestamp: timestamp("timestamp").notNull().defaultNow(),
  notes: text("notes"), // Used also for storing incidence description
  location: text("location"),
  device: deviceEnum("device").notNull(),
  concept: conceptEnum("concept").notNull(),
  application: text("application").notNull().default("Fichajes"), // Default application name
  isIncidence: text("is_incidence").notNull().default("false"), // Could be a boolean but stored as text to align with Drizzle's constraints
  createdAt: timestamp("created_at").defaultNow().notNull()
})

export const timeEntryCancellations = pgTable("time_entry_cancellations", {
  id: text("id")
    .primaryKey()
    .$defaultFn(() => createId()),
  timeEntryId: text("time_entry_id")
    .notNull()
    .references(() => timeEntries.id),
  cancelledBy: text("cancelled_by")
    .notNull()
    .references(() => users.id), // User or Admin who cancelled
  cancellationReason: text("cancellation_reason").notNull(),
  cancelledAt: timestamp("cancelled_at").defaultNow().notNull()
})
```

## Key Changes:

This schema ensures better data structure, consistency, and scalability.

### Enums for Consistency:

- Introduced pgEnum for type, device, and concept fields to ensure data integrity and consistency.

### Notes for Incidences:

- The notes field will now also store descriptions of incidences when they occur.

### NEW FIELDS in "time_entries" table:

- device: Stores the type of device used for the time entry.
- concept: Captures the reason for the time entry (work, training, break, lunch, other).
- application: Identifies the app associated with the entry, defaulting to "Fichajes".
- isIncidence: A boolean (stored as text) to flag when an entry is an incidence.

## NEW TABLES:

- There is also a new table "time_entry_cancellations" which will be used to store the cancellations of the time-entries.

### ✅ Pros:

- Separation of Concerns: time_entries table remains clean and only tracks valid time logs.
- Avoids NULL Values: Only cancelled entries have corresponding rows in the time_entry_cancellations table.
- Extensibility: We can track additional data such as cancelledBy (who cancelled it) and potentially support multiple cancellation events in the future.
- Better Data Integrity: Avoids unnecessary fields in the main table, ensuring only relevant data exists.

### ❌ Cons:

- More Complex Queries: Requires a join to fetch cancellation data along with time entries.
- Slightly Worse Performance for Reads: Fetching cancellations requires querying two tables instead of one.

## GOALS:

1. Modify the current schema to reflect all the new changes, add the new "time_entry_cancellations" table, and add the new fields to the "time_entries" table.
2. Update existing code or add new code to use the new schema to fulfill the new requirements:
   1. provide new seed data script to add data to all tables to test the new requirements
   2. lib/time-entries-utils.ts
   3. server actions
   4. components and UI
   5. hooks

## CONSTRAINTS:

- The component "EventRegistrationControlPanel" must be keep current design and functionality, but refactored to use the new schema and new requirements. Specially the "EventRegistrationControlPanel" form, which must preserve the current design and functionality, but refactored to use the new schema and new requirements.
- The component "CurrentDay" must keep current design and functionality, but refactored to use the new schema and new requirements. Specially the "CurrentDay" form, which must preserve the current design and functionality, but refactored to use the new schema and new requirements. Specially the "PendingDaysAlert" component, which must be refactored to use the new schema and new requirements and list all incidences pending to be registered from previous days to the current day.
- The buttons included in the "CurrentDay" component must be refactored to use the new schema and new requirements. Specially the "Start Day", "Start Break", "End Break", "End Day" buttons, which must be refactored to use the new schema and new requirements.

---

# 1. Refactor: New Hamburger Menu for Mobile with ShadcnUI Drawer component

Context:
@sidebar
@https://ui.shadcn.com/docs/components/drawer

I need to refactor the sidebar menu so in the case of being displayed on mobile devices the design is the following:

- the current design of the sidebar is hidden
- and we display the menu as a navbar on the top of the screen with a hamburger menu icon to the left of the screen, and the theme toggle button to the right of the screen, and the user avatar to the right edge of the screen. Like the design on the image attached.
- when the hamburger menu icon is clicked, the menu options with all the links are displayed using the shadcn "drawer" component that slides in from the bottom of the screen with a slide-in animation.
- when the user selects an option from the drawer, the drawer closes and opens the page associated to the option.
- when the drawer is open, we can tap outside the drawer and it will close.

Pay special attention to HTML and CSS to make sure the design is responsive and works on all mobile devices.

Current implementation:
[@sidebar code here]

Goals:

1. Create a new navbar with the hamburger menu to be shwon only on mobile devices
2. Keep the current sidebar as it is right now for larger devices and screens
3. Use the shadcn "drawer" component to display the menu
4. Use nice slide-in animation from the bottom to display the drawer
5. Use slide-down animation to hide it
6. Make sure to not change the design of the current sidebar

---

let's do some refactor of the project with a new feature. We are going to change the behavior of the app in terms of having a new hamburger menu to provide navigation for mobile devices, and we will maintain the current sidebar for larger devices and screens.

When clicked the menu will display a shadcn "drawer" component to display all the current menu options. Please use the image design refernce of how i want it to look.

Please use nice slide-in animation from the bottom to display the drawer, and slide-down animation to hide it.

Please make sure to not change the design of the current sidebar

---

# 3. New feature: add user management by admin and signup and sigin with Clerk

Context:
@app  
@sidebar

"I need to implement [feature name]. Here are the details:

- Business requirements: [list]
- Technical constraints: [list]
- Existing components: [list]
- Expected behavior: [description]"

---

I need to implement User Management. Here are the details:

1. Business requirements:

- Users must have personal profiles where they can clock in and out, request absences, see colleague availability, and access statistics.

- Users can belong to a project group or department for data organization.

- User access management should be handled by an admin.

- Users must sign up via Clerk and be manually approved before accessing the application.

- Pending users will see a message: "Your account is pending to be approved."

- Admins can approve, reject, or block users via a management dashboard.

- Approved users can log in and be redirected to the dashboard.

- The application should maintain a real-time status of user activity.

2. Technical constraints:

- Authentication and user management must be handled via Clerk.

- The admin dashboard must display all users categorized as Pending, Active, or Blocked.

- User statuses (working, on break, not working) must be updated in real time.

- The database must store the following user attributes:

  - User Name
  - Email
  - Role (Admin, Manager, Employee)
  - Status (Pending, Active, Blocked)
  - Last login
  - Date created
  - Date updated

- Admins should have the ability to edit user information where necessary.

- Admins should have the ability to delete users.

3. Existing components:

- Clerk authentication and user management system.

- Admin dashboard with sections for pending, active, and blocked users.

- User profile pages displaying work history and current status.

4. Expected behavior:

- Users sign up via Clerk and get redirected to the application, to a page where they see a message "Your account is pending to be approved by the admin".

- There must be an admin dashboard with a User Management page for admins to review pending users and approve or reject them.

- Approved users can log in and access the routes of the application allowed for users.

- Admins can block users, preventing them from logging in, but not deleting them from the database. Blocked users will see a message "Your account is blocked by the admin".
- Admins can unblock users, allowing them to log in again.
- Admins can edit user information where necessary.
- Admins can delete users.

---

# 2. Improve the UI of the barcharts used in the dashboard

Context:
@dashboard
@worked-hours-chart.tsx
@https://ui.shadcn.com/charts

"I need to refactor the barchart graphs used in the dashboard page because in current implementation they are having a layout problem. As you can see in the image attached they go way off the screen.

Current implementation:
[@barchart code here]

Reference image:
[@reference image here]

Reference code:

```typescript
"use client"

import { TrendingUp } from "lucide-react"
import { Bar, BarChart, CartesianGrid, LabelList, XAxis } from "recharts"

import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle
} from "@/components/ui/card"
import {
  ChartConfig,
  ChartContainer,
  ChartTooltip,
  ChartTooltipContent
} from "@/components/ui/chart"
const chartData = [
  { month: "January", desktop: 186 },
  { month: "February", desktop: 305 },
  { month: "March", desktop: 237 },
  { month: "April", desktop: 73 },
  { month: "May", desktop: 209 },
  { month: "June", desktop: 214 }
]

const chartConfig = {
  desktop: {
    label: "Desktop",
    color: "hsl(var(--chart-1))"
  }
} satisfies ChartConfig

export function Component() {
  return (
    <Card>
      <CardHeader>
        <CardTitle>Bar Chart - Label</CardTitle>
        <CardDescription>January - June 2024</CardDescription>
      </CardHeader>
      <CardContent>
        <ChartContainer config={chartConfig}>
          <BarChart
            accessibilityLayer
            data={chartData}
            margin={{
              top: 20
            }}
          >
            <CartesianGrid vertical={false} />
            <XAxis
              dataKey="month"
              tickLine={false}
              tickMargin={10}
              axisLine={false}
              tickFormatter={(value) => value.slice(0, 3)}
            />
            <ChartTooltip
              cursor={false}
              content={<ChartTooltipContent hideLabel />}
            />
            <Bar dataKey="desktop" fill="var(--color-desktop)" radius={8}>
              <LabelList
                position="top"
                offset={12}
                className="fill-foreground"
                fontSize={12}
              />
            </Bar>
          </BarChart>
        </ChartContainer>
      </CardContent>
      <CardFooter className="flex-col items-start gap-2 text-sm">
        <div className="flex gap-2 font-medium leading-none">
          Trending up by 5.2% this month <TrendingUp className="h-4 w-4" />
        </div>
        <div className="leading-none text-muted-foreground">
          Showing total visitors for the last 6 months
        </div>
      </CardFooter>
    </Card>
  )
}
```

Goals:

1. Improve the UI of the barcharts
2. Make sure the barcharts are responsive and fit the screen size
3. Make sure the barcharts are not going off the screen
4. Make sure you use the shadcn "bar-chart" component to display the barcharts (https://ui.shadcn.com/charts)

---

# EXAMPLES of feature or refactor tasks

## Refactor: XXX

Context:
@app

"I need to refactor [component] because [reason].
Current implementation:
[paste code]

Goals:

1. [list goals]
2. [list constraints]
3. [list requirements]"

---

Haz un planteamiento de como implementar un algoritmo en pseudocódigo explicativo para el siguiente requisito funcional para el cómputo de horas de una aplicación de control de asistencia.

Requisito funcional:

- El usuario debe poder registrar su entrada y salida de la oficina.
- El usuario debe poder registrar salidas y entradas de la oficina ofreciendo varios motivos tipados (desayuno, comida, formación, otro).

Ejemplo:

| Hora de Registro | Entrada   | Salida    |
| ---------------- | --------- | --------- |
| 8:00             | JORNADA   |           |
| 11:00            |           | Desayuno  |
| 11:30            | Desayuno  |           |
| 14:00            |           | Comida    |
| 14:30            | Comida    |           |
| 15:30            | JORNADA   |           |
| 15:30            | Formación |           |
| 16:30            |           | Formación |

suma de salidas - suma de entradas = (11+14+15,5+16,5)-(8+11,5+14,5+15,5) = 57 - 49,5 = 7,5
