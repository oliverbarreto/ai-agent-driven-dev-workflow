# Feature: Display Time Entry Locations on a Map in Next.js App

We need to continue developing functionality tasks and now we want to add the next functionality.

## Overview

We want to add functionality to enhance the time entry table (/registros) by adding a location-based feature using the library "Google Maps API".

Each time entry in the table already has a location column (a text string in the database with latitude and longitude), which we want to modify to include, if location is available, an interactive map icon that, when clicked, will show a google map inside a Shadcn UI modal allowing users to view the location on a map in a modal.

Keep in mind the case where the location for the time entry is unavailable (saved in the database as "Unknown"). In such cases, the map icon should not be shown. In those cases, the location field should be shown as "-".

Documentation:

1. You have access to a tutorial at @"google*maps_api.md" document and the full Google Maps API documentation of the library at https://web.archive.org/web/20230701010714mp*/https://react-google-maps-api-docs.netlify.app/#section-introduction.

2. Creating an Interactive Map with the Google Maps API in Next.js - Example https://dev.to/adrianbailador/creating-an-interactive-map-with-the-google-maps-api-in-nextjs-54a4

3. Official Documentation of Google Maps API: https://react-google-maps-api-docs.netlify.app/

## GOALS:

The goal is to add functionality to display a map icon in the location column only if the location field is available. To do this, we will:

0. Create a new Project in Google Cloud Console and get an API key.

1. Install the dependencies:

   - Install the library `@react-google-maps/api` (npm install --save @react-google-maps/api).

2. Modify the Frontend Table in "/registros" page
   - Display a map icon in the location column only if the location field is available. If the location field is not available, the map icon should not be shown, and instead of the map icon we must show "-" in the location column as not available.
   - The icon should be clickable to open a nice Shadcn UI modal.
3. Implement the Modal page:
   - Use the google maps api library to display a map inside the modal.
   - While loading the map, show a loading spinner.
   - When opened, the modal should:
     - Center the map on the latitude and longitude of the time entry.
     - Show a marker at the entry's location. Use the standard pin icon as marker.
     - Close the modal when the user clicks outside or on a close button.
   - Style the Modal: Ensure it is responsive and styled with TailwindCSS.
4. Error Handling & Edge Cases
   - If the location field is not available or undefined, do not render the map icon on the table.
   - If the map fails to load, show a fallback message (e.g., “Map unavailable”).
5. Technical Considerations
   - Always ask to Install Dependencies: Use `react-google-maps/api` for map rendering (npm install --save @react-google-maps/api).

## REQUIREMENTS:

- Take into account that the location, when available, is given in the format "latitude,longitude" as text string in the database (eg "28.46571922090483,-16.262760478583765"). When not available, the location field is stored as "Unknown" in the database.

## CONSTRAINTS:

- Do not install or run commands on the composer. Always ask me to install any dependency or run commands on the terminal
- Do not create or modify any other functionality, design or file other than the ones required to add the new functionality.
- Use the library `@react-google-maps/api` for map rendering.
- Optimize Performance: take into account the way we should load the maps dynamically (next/dynamic) to avoid issues with SSR.
- Style the Modal: Ensure it is responsive and styled with TailwindCSS and Shadcn UI.
- Ensure that it is mobile friendly and responsive.

--- PROMPT ---

Please continue to build this functionality step by step and use the scratchpad to annotate your reasoning and progress, and to keep track of the tasks. Also use the scratchpad to write down any important lessons learned after the process.

I already created the project in Google Cloud Console and got the API key which is now in the `.env.local` file in the variable `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY`.

---

# Scratchpad

Current Task: Implementing Google Maps Location Feature

## Overview

Adding functionality to display time entry locations on a map using Google Maps API. The location will be shown as a clickable map icon in the time entries table that opens a modal with the location on a map.

## Implementation Steps

[x] 1. Install Dependencies - Installed @react-google-maps/api package

[x] 2. Create Map Modal Component - Created new MapModal component in src/components/ui/map-modal.tsx - Implemented loading state with Loader2 spinner - Added error handling for map loading failures - Styled modal with Shadcn UI Dialog and TailwindCSS - Added proper TypeScript types and documentation

[x] 3. Modify Time Entries Table - Added MapPin icon from Lucide to location column when available - Replaced text location with icon + modal trigger - Handle "Unknown" location case by showing "-" - Integrated MapModal component with state management

[x] 4. Fix Google Maps Integration Issues - Created GoogleMapsProvider component to prevent multiple script loads - Moved LoadScript to root layout - Fixed error handling in MapModal - Improved modal state management

[ ] 5. Testing & Optimization - Test with different location formats - Test error cases (no location, invalid coordinates) - Ensure mobile responsiveness - Optimize map loading performance
