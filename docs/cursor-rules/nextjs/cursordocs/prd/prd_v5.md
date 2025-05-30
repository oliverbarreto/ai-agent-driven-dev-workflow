# Feature: Phase 4: New functinoality to create "Recent Absences" component.

## Overview

- [ ] Add new functionality to create a new "Incidence List" component. We should divide this component into two sections:

  - [ ] Recent Absences: It should display a list of all "absences" for the current user: that is days without any time entry at all;
  - [ ] Uncompleted Days: which are dates with at least one unfinished session, work/training or any other type, lunch, medical, break, other, etc.

There will be stats on the page /jornadas in the component "event-registration-control-panel.tsx" to display the total number of absences and uncompleted days that should be updated when the user registers or cancels a time entry.

SECTION 1: Recent Absences

- [ ] It should display a list of all absences for the current user: that is, it should display a list with all days without any time entry at all.

  - [ ] The section should have a header with the title "Recent Absences" and a description with the text "These are the days without any time entry at all."
  - [ ] The section should have a stat on the header showing the total number of absences.
  - [ ] The list should show the date in a format like "lunes, 10 de febrero de 2025"
  - [ ] Every row in the list should have a button to open a form to register an time entry. For this, we should try to reuse the form that we already have and use in "current-day.tsx" and be prefilled with the date of the day to register the time entry.
  - [ ] When the user registers a time entry, the "Incidence List" MUST BE updated automatically.

SECTION 2: Uncompleted Days:

- [ ] It should display a list of all dates with at least one unfinished session, work/training or any other type, lunch, medical, break, other, etc.

  - [ ] Take into account that unfinnished sessions can be both, a "start" time entry with no "end" for the same concept, and viceversa. For example: 09:00 start work, 14:00 end work, and 15:00 start lunch, 16:00 end lunch. 16:00 start work. In this case, the day is uncompleted because the lunch is not finished.There should be a for example 17:30 end work to be completed.
  - [ ] The section should have a button to open a form to register an time entry, and be prefilled with the date of the day to register the time entry, and the type of time entry to register (start or end) and the concept (work, training, lunch, medical, break, other, etc.).

  - [ ] The section should have a header with the title "Uncompleted Days" and a description with the text "These are the days with at least one unfinished session of the same concept"
  - [ ] The section should have a stat on the header showing the total number of dates with at least one unfinished session of the same concept.
  - [ ] The list should show the date in a format like "lunes, 10 de febrero de 2025"
  - [ ] Every row in the list should have a button to open a form to register an time entry. For this, we should try to reuse the form that we already have and use in "current-day.tsx" and be prefilled with the date of the day to register the time entry.
  - [ ] When the user registers a time entry, the "Incidence List" MUST BE updated automatically.

## GOALS:

- [x] Add the route for "/incidencias"
- [x] Analyze the schema and current logic to create a service to:

  - [x] calculate the total number of absences.
  - [x] calculate the total number of uncompleted days.
  - [x] update the "Incidence List" when a time entry is registered.
  - [x] update the "Incidence List" when a time entry is cancelled.

- [x] Create the page for the route with an independent component with the UI that displays the "Incidence List" based on the design of the "current-day.tsx" list for "registered events"

  - [x] This component should be independent and not use the "current-day.tsx" component.
  - [x] This component should have also two different components, one for the "Recent Absences" section and one for the "Uncompleted Days" section.

- [x] add a stat label to the "event registration control panel" to show the total number of absences and uncompleted days. When clicked on any of these two new stats, it should navigate to the "Incidence List" (/incidencias) page.

## REQUIREMENTS:

- [ ] try to separate the logic and the way we calculate the stats to allow easily adding the new stats to the UI in /jornadas page.
- [ ] Let's use a similar design and layout for the "Uncompleted Days" section as the "Recent Absences" section. It should be based on the design of "Registered Events" section in the "current-day.tsx" component that you can see as example in the image.
- [ ] Ensure that it is mobile friendly and responsive.
- [ ] It is a must-have functionality to update the "Incidence List" when a time entry is registered or cancelled in other parts of the "/(users)/jornada/page.tsx" page and every time we load the page.

## CONSTRAINTS:

- [ ] DO NOT CHANGE the design or functionality of any other component just the required code to fulfill this feature.
- [ ] If you need to THE CURRENT DESIGN OF THE "Recent Absences" section.

- [ ] Do not install or run commands on the composer. Always ask me to install any dependency or run commands on the terminal
- [ ] Do not create or modify any other functionality, design or file other than the ones required to add the new functionality.

--- PROMPT ---

Let's start to build this functionality step by step and use the scratchpad to annotate your reasoning and progress, and to keep track of the tasks. Also use the scratchpad to write down any important lessons learned after the process.

---

# Implementation Notes

## Implementation Steps

[x] 1. Install Dependencies - Installed @react-google-maps/api package

[x] 2. Create Map Modal Component - Created new MapModal component in src/components/ui/map-modal.tsx - Implemented loading state with Loader2 spinner - Added error handling for map loading failures - Styled modal with Shadcn UI Dialog and TailwindCSS - Added proper TypeScript types and documentation

[x] 3. Modify Time Entries Table - Added MapPin icon from Lucide to location column when available - Replaced text location with icon + modal trigger - Handle "Unknown" location case by showing "-" - Integrated MapModal component with state management

[x] 4. Fix Google Maps Integration Issues - Created GoogleMapsProvider component to prevent multiple script loads - Moved LoadScript to root layout - Fixed error handling in MapModal - Improved modal state management

[ ] 5. Testing & Optimization - Test with different location formats - Test error cases (no location, invalid coordinates) - Ensure mobile responsiveness - Optimize map loading performance

## Progress Tracking

Current Status: Implementation phase - Core functionality completed and initial bugs fixed
Next Step: Final testing and optimization

# Tasks

## Current Task: Phase 4 - Recent Absences Component

### Overview

Building a new "Incidence List" component with two main sections:

1. Recent Absences - Days without any time entries
2. Uncompleted Days - Days with unfinished sessions

### Implementation Plan

#### Step 1: Route and Basic Structure

- [x] Create route "/incidencias"
- [x] Create basic page component structure
- [x] Create RecentAbsencesList component
- [x] Create UncompletedDaysList component
- [x] Set up layout and navigation integration

#### Step 2: Data Layer

- [x] Analyze current schema for required queries
- [x] Create service functions for:
  - [x] Calculating total absences
  - [x] Calculating uncompleted days
  - [x] Fetching absence data
  - [x] Fetching uncompleted days data
  - [x] Real-time updates on time entry changes

#### Step 3: UI Components

- [x] Create IncidenceList container component
- [x] Create RecentAbsences section component
  - [x] Header with title and stats
  - [x] List component for absences
  - [x] Integration with time entry form
- [x] Create UncompletedDays section component
  - [x] Header with title and stats
  - [x] List component for uncompleted sessions
  - [x] Integration with time entry form

#### Step 4: Stats Integration

- [x] Add stats to event registration control panel
- [x] Implement navigation to /incidencias on stat click
- [x] Set up real-time updates for stats

### Progress

Completed Step 1: Basic Structure

- [x] Created route "/incidencias"
- [x] Created basic page component structure
- [x] Created RecentAbsencesList component
- [x] Created UncompletedDaysList component
- [x] Set up layout and navigation integration

Completed Step 2: Data Layer

- [x] Analyze current schema for required queries
- [x] Create service functions for:
  - [x] Calculating total absences
  - [x] Calculating uncompleted days
  - [x] Fetching absence data
  - [x] Fetching uncompleted days data
  - [x] Real-time updates on time entry changes

Completed Step 3: UI Components

- [x] Create IncidenceList container component
- [x] Create RecentAbsences section component
  - [x] Header with title and stats
  - [x] List component for absences
  - [x] Integration with time entry form
- [x] Create UncompletedDays section component
  - [x] Header with title and stats
  - [x] List component for uncompleted sessions
  - [x] Integration with time entry form

Completed Step 4: Stats Integration

- [x] Add stats to event registration control panel
- [x] Implement navigation to /incidencias on stat click
- [x] Set up real-time updates for stats

---

## Current Task: Phase 4 - Recent Absences Component

### Overview

Building a new "Incidence List" component with two main sections:

1. Recent Absences - Days without any time entries
2. Uncompleted Days - Days with unfinished sessions

### Implementation Plan

#### Step 1: Route and Basic Structure

- [x] Create route "/incidencias"
- [x] Create basic page component structure
- [x] Create RecentAbsencesList component
- [x] Create UncompletedDaysList component
- [x] Set up layout and navigation integration

#### Step 2: Data Layer

- [x] Analyze current schema for required queries
- [x] Create service functions for:
  - [x] Calculating total absences
  - [x] Calculating uncompleted days
  - [x] Fetching absence data
  - [x] Fetching uncompleted days data
  - [x] Real-time updates on time entry changes

#### Step 3: UI Components

- [x] Create IncidenceList container component
- [x] Create RecentAbsences section component
  - [x] Header with title and stats
  - [x] List component for absences
  - [x] Integration with time entry form
- [x] Create UncompletedDays section component
  - [x] Header with title and stats
  - [x] List component for uncompleted sessions
  - [x] Integration with time entry form

#### Step 4: Stats Integration

- [x] Add stats to event registration control panel
- [x] Implement navigation to /incidencias on stat click
- [x] Set up real-time updates for stats
