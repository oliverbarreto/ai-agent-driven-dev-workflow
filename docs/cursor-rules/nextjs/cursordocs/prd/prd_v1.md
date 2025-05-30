# Objective

The goal is to create a SaaS application to offer multiple clients (organizations) a solution for time tracking employee clock-in management.
Example of similarapps:

- https://www.stelorder.com/tempo/
- https://www.sesametime.com/#
- https://www.toggl.com/

# Technology Stack

This project should use: NextJS 15 with App router and src folder. It should use Server Components, Server Acctions, and SSR over API routes.

It also will use Tailwind CSS, Shadcn, Lucide Icons, Zustand, and Zod. As database it will use Neon Postgres Service (https://neon.tech/) with Drizzle as ORM. Clerk for Auth

# Functional Requirements

The functional requirements of the application are:

## Users

All users have a personal profile where they can clock in and out of work, request absences, see if other colleagues are working, and access various statistics.

Users can belong to a project group or department, which will later be used to organize the visualization and accounting of data.

### User management

The user management will have the following features:

Users can login via Clerk and then they will be redirected to the application. In the application they will be able to see their profile information and their workdays history.

In this stage of the project, the user management will be done manually by the admin user. All users will signup into the application and the admin will have to manually accept them as valid users of the application. Once the user signsup with clerk will be redirected to the application and will see a message "Your account is pending to be approved". All pending users will be listed in the admin dashboard, in a section with the list of all users, pending users and active users. There will also be functionality to "Block" users and suspend their ability to log into the applications. The admin will be able to approve or reject them on the user management page.

Once users are accepted, they will be able to login into the application and they will be redirected to the dashboard.

The application will have the following information about the users:

- User Name
- Email
- Role (Admin, Manager, Employee)
- Status (Pending,Active, Blocked)
- Last login
- Date created
- Date updated

The admin will be able to see all the information about the users and will be able to edit some of the information.

The application will also have information about the current status of every user. This will be used to see if a user is working, on a break, or if they are not working at the moment. It has to be updated in real time according to the events that are being tracked by the application.

## Workday Time Tracking

The application will have a real time clock-in/clock-out system that will be used to track the time of the users, allowing Employees to log their workday: clock-in time, clock-out time, lunch breaks, rest periods, and pauses, with the ability to add notes and images.

We have the following events:

- Start Day or Work Session: start
- End Day or Work Session: end
- Start Break: break_start
- End Break: break_end

It will have a button to start a work sesion, and a button to end a work session. It will also have a button to start a break, and a button to end a break.

In the case of

It should also be a good feature to register the location from which employees check in or out. This information will be stored in the database and will be displayed in when showing events of the user's time entries in the application.

The application will identify the type of device that is being used to clock in and will also store in the database that information (computer or mobile). This information has to be shown on the registry page with all the entries for all users events.

### Use case for the time tracking

When interacting with the application:

- the employee can start a work session with a start event. An employee can have as many work sessions in the day as he wants.
  - The employee must always end all work sessions in the day, so the system can calculate the total time worked in the day.
  - There will be a warning if the employee does not end one or more work sessions in the day.
- the employee can have as many breaks as he wants but he always need to start and end a break in the day.
  - The employee must always end all breaks in the day, so the system can calculate the total time worked in the day.
  - There will be a warning if the employee does not end one or more breaks in the day.
- The system must allow the employee to register events for a day and time in different day (later day)

  - for example: the system must allow the case that an employee does not register a break end or the end of a day, and the next day he can register the missing events.
  - therefore the system should warn the user that there are pending events to register on the system. Please provide nice ui for "fixing" events pending of preivous days. The application must indicate the number of days still pending to be registered correctly

- The dialog to fix ending previous days needs to allow to enter a date (day, month, year) and time (hour and minutes) and should create a valid time entry in the database.

- If the employee should have various days to fix, the system should list them and allow fixing them one by one with the form.

### Register Entry Events Component:

The way users will register event entries to clock in and out will be using a component that will be shown in the dashboard of the user. This component will only have the responsability to provide the interface to interact with the application to register events.

The component will have the following features:

- Show the current time
- Show the time of the first start of the day
- Show the time worked in the day
- Show a button to register an event, which will show a modal form. The form will have the following fields:

  - Event Date: the date of the event with day, month and year fields. It should be enabled but preloaded with the current date when the form is displayed. It will use the Shadcn Date Picker component.
  - Event Time: the time of the event with hour and minute fields. It should be preloaded with the current time when the form is displayed. It will use the Shadcn dropdown selection component and preloaded with 30 minutes intervals to choose from the 24 hour day.
  - the type of event that the employee wants to register. It will be a shadcn radio group with all the possible event types: start work session, end work session, start break, end break
  - It will have a text area to add notes to the event
  - It will have a button to submit the event and a button to cancel the form.

### Future Features:

1. FUTURE FEATURE: the admin of the application can define a threshold of time that will be used to determine if the displayed time for the day is below the threshold. If the time is below the threshold, the application will show the time in black color. If the time is above the threshold, the application will show the time in orange color.

2. FUTURE FEATURE: The application, if possible, will also store the location of the user (latitude and longitude). This information will be used to see if a user is working from home or from the office.

3. FUTURE FEATURE: add an image uploader to the event

## Absences

The application must allow the management of employee absence periods. Absences may be managed in an external system, but it is necessary to incorporate vacation periods, sick leave, or absences for various reasons, ensuring visibility of whether daily clock-ins require justification.
Absences can be viewed on a calendar for efficient planning and organization.

## Clock-In Management for Administration

The application should provide organization managers access to employee clock-in information. It will present data in a way that allows for an overview at a glance using a timeline.
Organize employees by departments and observe the details of their workdays.
The Tempo timeline is interactive, allowing users to move forward and backward in time.
Employee absences will also be reflected.

## Calendars

The application will allow the configuration of calendars by defining holidays and restricted workdays for employees. Users may have different assigned calendars based on their location and local holidays.
The application should enable the assignment of calendars to users in bulk, individually, or customized by groups.

## Clock-In Dashboard

This is the dashboard where employees can see a summarized view of all their activities. It will have various sections or components:

- User: Displays user information such as name, surname, and email.
- Your Worked Hours: A graphical representation of worked hours over the week, month, and year.
- Your Workday: Includes details on start time, breaks, resumptions, and workday completion. It will have action buttons to log - these events.
- Your Absences: Shows pending absences and their respective reasons.

## Dashboard for Managing Your Team’s Workdays

Employee workdays will be recorded in a history log that can always be accessed.
Easily see at a glance who is working or on a break.
Download reports or apply filters to monitor employee work schedules.
