# Scratchpad

## Current Task/Objective:

- [x] Implement the "Calendarios" tab in the settings area with a nested vertical tab menu for "Calendarios Festivos" and "Calendarios Laborales"
- [x] Implement the "Calendarios Laborales" functionality with data model, logic, and UI
- [x] Implement the "Calendarios Festivos" functionality with data model, logic, and UI
- [x] Fix tab selection in settings layout for calendarios pages

## Implementation:

### Analysis:

- [x] The task is to create a skeleton for the "Calendarios" tab in the settings area
- [x] The tab should have a sub-layout with a nested vertical tab menu
- [x] The nested tabs should be "Calendarios Festivos" and "Calendarios Laborales"
- [x] We need to create the layout structure only, without implementing the actual functionality yet
- [x] The route for this tab is http://localhost:3000/admin/settings/calendarios
- [x] The task is to implement the "Calendarios Laborales" tab functionality
- [x] This includes creating the data model, server actions, queries, and UI
- [x] The feature allows users to create and manage holiday calendars
- [x] Each calendar has a name, year, and a list of holiday dates
- [x] Holiday dates have a name, date, type, and active status
- [x] Users can import holidays via CSV or add them manually
- [x] The UI should display a table of calendars with counts by holiday type
- [x] Implement the "Calendarios Festivos" functionality
- [x] Create a system for managing holiday calendars that can be associated with labor calendars
- [x] Allow importing holiday dates from labor calendars for specific years
- [x] Display a calendar view with all holidays marked
- [x] The issue was in the `settings-tabs.tsx` file where the `getActiveTab()` function didn't handle calendarios paths
- [x] The function only handled special cases for locations and departments
- [x] When in calendarios pages (festivos or laborales), the "Empresa" tab was always selected as default

#### Current Database Schema Analysis:

- [x] There are existing `calendars` and `calendarEvents` tables in the schema
- [x] The `calendars` table has id, organizationId, name, and createdAt fields
- [x] The `calendarEvents` table has id, calendarId, type, date, name, and createdAt fields
- [x] The schema needs to be extended to support the new requirements
- [x] New tables needed: `holidayCalendars` and `holidayCalendarAssociations`

#### Implementation Requirements:

- [x] Extend the database schema to support the new requirements
- [x] Create server actions for CRUD operations on calendars and holiday dates
- [x] Implement CSV import functionality
- [x] Create UI components for the calendar list and holiday date management
- [x] Implement the modal for adding holiday dates manually

#### Data Model Considerations:

1. **Schema Extension Options:**
   - Option 1: Extend existing `calendars` table with a year field
   - Option 2: Create a new `holidayCalendars` table specifically for this feature
2. **Holiday Type Handling:**

   - Option 1: Store counts in the calendar table (denormalized for performance)
   - Option 2: Calculate counts at runtime (normalized but potentially slower)
   - Option 3: Use materialized views or caching for the best of both worlds

3. **Decision on Holiday Type Counts:**

   - Pros of storing counts in the calendar table:
     - Faster retrieval for the table view
     - Reduces computation when displaying the list
     - Simplifies queries for the main calendar list
   - Cons of storing counts:
     - Requires updating counts when holiday dates change
     - Introduces potential data inconsistency
     - Adds complexity to the data model
   - Pros of calculating at runtime:
     - Always accurate and consistent with actual data
     - Simpler data model
     - No need to maintain count fields
   - Cons of calculating at runtime:
     - Potentially slower for large datasets
     - More complex queries
     - May impact performance on the main calendar list page

4. **Decision:**
   - Extend the existing `calendars` table with a year field
   - Add active status to `calendarEvents` table
   - Calculate holiday type counts at runtime initially
   - If performance becomes an issue, implement caching or consider denormalization

#### Implementation Plan:

1. **Database Schema Updates:**

   - [x] Add `year` field to the `calendars` table
   - [x] Add `active` and `updatedAt` fields to the `calendarEvents` table
   - [x] Create an enum for holiday types (Nacional, Autonómico, Local, Empresa)

2. **Server Actions:**

   - [x] Create action to create/update calendars
   - [x] Create action to add/update/delete holiday dates
   - [x] Create action to import holiday dates from CSV
   - [x] Create action to toggle holiday date active status

3. **UI Components:**

   - [x] Create calendar list table component
   - [x] Create calendar creation/edit modal
   - [x] Create holiday date list component
   - [x] Create holiday date creation/edit modal
   - [x] Create CSV import component

4. **Integration:**
   - [x] Connect UI components with server actions
   - [x] Implement client-side validation
   - [x] Add error handling and loading states

#### List of Tasks:

- [x] Create a calendarios-tabs.tsx component for the nested vertical tab menu
- [x] Create a layout.tsx file for the "Calendarios" tab
- [x] Create a festivos/page.tsx file for the "Calendarios Festivos" tab
- [x] Create a laborales/page.tsx file for the "Calendarios Laborales" tab
- [x] Update the main page.tsx to redirect to the first nested tab
- [x] Update database schema
- [x] Create server actions for calendar management
- [x] Create server actions for holiday date management
- [x] Create server action for CSV import
- [x] Implement calendar list UI
- [x] Implement calendar creation/edit modal
- [x] Implement holiday date list UI
- [x] Implement holiday date creation/edit modal
- [x] Implement CSV import UI
- [x] Add validation and error handling
- [x] Test the complete functionality

## Current Progress

We have successfully implemented the "Calendarios Laborales" functionality with the following components:

1. **Database Schema**:

   - Extended the `calendars` table with a `year` field and `updatedAt` timestamp
   - Added `active` status and `updatedAt` timestamp to the `calendarEvents` table
   - Created a `holidayType` enum for the different types of holidays

2. **Server Actions**:

   - Implemented CRUD operations for calendars (create, update, delete)
   - Implemented CRUD operations for holiday dates (add, update, delete)
   - Implemented CSV import functionality
   - Implemented a function to get holiday type counts

3. **UI Components**:
   - Created a calendar list component that displays calendars with their holiday type counts
   - Created a calendar creation modal with form validation
   - Created a calendar edit modal for updating existing calendars
   - Created a calendar detail page for managing holiday dates
   - Created a holiday date creation modal with form validation
   - Created a holiday date edit modal for updating existing holiday dates
   - Created a CSV import component with file validation and data preview

We have now also successfully implemented the "Calendarios Festivos" functionality with the following components:

1. **Database Schema**:

   - Created a new `holidayCalendars` table with fields for id, organizationId, name, createdAt, and updatedAt
   - Created a new `holidayCalendarAssociations` table to track associations between holiday calendars and labor calendars, with fields for id, holidayCalendarId, calendarId, year, createdAt, and updatedAt
   - Set up proper relations between these tables and the existing tables

2. **Server Actions**:

   - Implemented CRUD operations for holiday calendars (create, update, delete)
   - Implemented functionality to associate labor calendars with holiday calendars for specific years
   - Implemented functions to get holiday dates for a given year from associated labor calendars
   - Implemented ability to remove associations between holiday calendars and labor calendars

3. **UI Components**:
   - Created a holiday calendar list component that displays holiday calendars with their associations
   - Created a holiday calendar creation modal with form validation
   - Created a holiday calendar detail page that shows the calendar for a specific year with holiday dates
   - Created a component to associate labor calendars with holiday calendars for specific years
   - Implemented a year-based calendar view that shows all 12 months with holiday dates marked
   - Added a legend to identify different types of holiday dates by color
   - Enhanced the UI to display holiday dates clearly and allow easy navigation between different years

## Next Steps

1. Test the complete functionality with real data, especially in the following scenarios:

   - Creating holiday calendars with different names and purposes
   - Associating multiple labor calendars with a holiday calendar for different years
   - Viewing holiday calendars for different years and verifying that dates are displayed correctly
   - Removing associations and verifying that the related holiday dates are no longer displayed

2. Potential enhancements:

   - Add the ability to manually add holiday dates directly to a holiday calendar (not just imported from labor calendars)
   - Implement filtering or search functionality for holiday calendars
   - Allow exporting holiday calendar data
   - Implement a user interface to apply holiday calendars to locations or groups of users

3. Documentation and training:
   - Create user documentation explaining the difference between "Calendarios Laborales" and "Calendarios Festivos"
   - Document the process for importing holiday dates from labor calendars
   - Train administrators on how to manage holiday calendars effectively

## Lessons Learned

1. When a feature is used in multiple places, it's important to identify all instances to maintain consistency
2. For modals that are used across different routes, consider creating a shared component
3. When adding new fields to existing functionality, check if the schema already supports it to avoid migrations
4. Using a shared component for modals helps maintain consistency in UI and functionality across the application
5. When updating functionality used in multiple places, it's important to update all instances to maintain feature parity
6. When displaying sensitive information like cancellation reasons, it's important to make it easily accessible but not overwhelming in the main UI
7. Using conditional rendering in dropdown menus helps keep the UI clean and contextual
8. When implementing search functionality, debouncing is important to prevent unnecessary API calls and improve performance
9. When adding new filters, it's important to maintain consistency with existing filter behavior
10. When implementing search functionality, consider all relevant fields that users might want to search by
11. When implementing file downloads, use proper MIME types and Content-Disposition headers
12. When handling large datasets, consider using streaming or pagination if needed
13. When implementing export functionality, ensure all relevant data fields are included in a clear format
14. When reusing components across different pages, ensure they maintain consistent behavior and styling
15. When detecting device types, use useEffect to avoid hydration mismatches
16. When adding new enum fields to existing tables, always provide a default value to handle existing records
17. Consider adding new fields as nullable first if we're not sure about the default value
18. Test form validation thoroughly when adding new required fields
19. When adding new fields to forms, make sure to update all components that use the form to handle the new field
20. When displaying icons in a list, maintain consistent sizing and spacing for better visual alignment
21. Use muted colors for secondary information icons to maintain visual hierarchy
22. When adding new columns to tables, ensure they follow the same sorting and styling patterns as existing columns
23. When adding new fields to types, make sure to update all related functions and components that use that type
24. When adding sortable columns, ensure the sorting logic handles default values consistently
25. When reorganizing navigation, ensure that links are updated in all relevant components (sidebar, mobile nav, etc.)
26. When creating tabbed interfaces, use consistent styling and behavior across all tabs
27. When moving pages to new locations, ensure all imports and paths are updated correctly
28. **Avoid using `window.location.reload()` for data refreshing** as it resets UI state including tab selection
29. **Use Next.js's `router.refresh()` combined with `router.push(pathname)`** to maintain UI state while refreshing data
30. **Use `revalidatePath()` with the correct path patterns** in server actions to ensure data is properly refreshed
31. **For dynamic paths in `revalidatePath()`, use template literals with actual values** instead of path patterns with placeholders
32. **Consider using root layout revalidation** (`revalidatePath('/', 'layout')`) for changes that affect multiple parts of the app
33. **In React Query, use `refetchOnMount: "always"` and `staleTime: 0`** to ensure data is always fresh
34. **Replace `cacheTime` with `gcTime` in React Query v4** for controlling garbage collection of unused queries
35. **Use direct SQL queries instead of query builders** when you need to ensure you're getting fresh data
36. **Add timestamps to API responses** to help with cache busting
37. **Invalidate queries after operations complete** using `queryClient.invalidateQueries()`
38. **Reset form state when dialogs open** to prevent stale data from being displayed
39. **Extract locationId/departmentId from pathname** when needed for query invalidation
40. **Add small delays before navigation** after data operations to ensure cache is refreshed
41. **Use client components for UI elements that need to respond to route changes** like tab selection
42. **Separate client and server components** to maintain clear boundaries and optimize performance
43. **Use `useEffect` to force refetch** when components mount to ensure fresh data
44. **Handle dialog state properly** by closing dialogs before refreshing data to prevent UI glitches
45. **When implementing nested tab navigation**, create a layout file to handle the nested tabs and ensure proper routing
46. **When deciding between storing calculated values vs. computing them at runtime**, consider the trade-offs between performance and data consistency
47. **For features that involve importing data (like CSV import)**, implement proper validation and error handling to ensure data integrity
48. **When extending database schemas**, create proper migration files to ensure consistent schema updates across environments
49. **When working with dates in database operations**, be careful about string vs. Date object conversions and timezone handling
50. **When implementing table UIs with counts or aggregated data**, consider the performance implications and potential caching strategies
51. **When fixing linter errors related to database queries**, make sure to use the correct column references and types from the schema
52. **When implementing database schema changes that involve enum types**, consider the following approaches:

- For new tables, define the enum type in the schema and use it directly
- For existing tables with data, use a migration strategy that handles type conversion properly
- When converting a column from one type to another (especially to an enum), use a temporary column approach or explicit USING clause
- If the feature is not yet in production, consider dropping and recreating the tables for a clean implementation
- Always test migrations in a development environment before applying them to production

53. **In Next.js 15, dynamic route parameters must be awaited before use**:

- Dynamic APIs like `params` and `searchParams` are now asynchronous in Next.js 15
- Always await the params object before accessing its properties: `const paramsObj = await params`
- This is a breaking change from Next.js 14 where params could be accessed directly
- The error "Route used `params.id`. `params` should be awaited before using its properties" indicates this issue
- This applies to all dynamic route parameters in layout.js, page.js, route.js, etc.

54. **When displaying dates in a UI, consider localization and consistent formatting**:

- Use date-fns with locale support for consistent date formatting across the application
- For Spanish applications, use the `es` locale from date-fns for proper month names and date formats
- Prefer explicit date formats (like "dd/MM/yyyy") over browser-dependent `toLocaleDateString()`
- Set weekStartsOn to 1 (Monday) for calendar components in European applications
- Ensure date formatting is consistent across all parts of the application for better user experience

55. **When using Drizzle ORM with related tables, always define relations explicitly**:

- Define relations using the `relations` function from Drizzle ORM for all related tables
- Missing relations can cause errors like "Cannot read properties of undefined (reading 'referencedTable')"
- Relations enable features like eager loading with the `with` option in queries
- Relations should be defined in the same file as the schema to ensure they're available
- When adding new tables, remember to add corresponding relation definitions

56. **When implementing calendar views, follow these best practices**:

- For multi-month displays, consider grid layouts that work well at different screen sizes
- Use color coding for different types of events/holidays for better visual identification
- Include a legend to explain color coding and any other visual indicators
- For year views, organize months in rows and ensure consistent day labeling (L,M,X,J,V,S,D for Spanish)
- Place supplementary information alongside the calendar rather than below it for better screen real estate usage
- Use vertical scrolling for lists of events rather than pagination when possible
- Implement date selection to allow users to see details about specific dates

57. **When working with date associations across different years**:

- Be careful with date adjustments when importing dates from one year to another
- Consider leap years when handling February 29th dates
- Store the association year separately from the actual event dates to maintain historical records
- Use a flexible data model that allows the same calendar to be used across multiple years
- Implement clear UI to show which years are available for a given calendar

58. **When implementing React components that manage relationships between data**:

- Use proper error handling when fetching related data
- Provide clear feedback when operations succeed or fail
- Keep the UI responsive even when loading large datasets
- Consider pagination or virtual scrolling for large lists
- Use dropdown selectors for choosing related items rather than free text entry

59. **When implementing tab navigation with nested routes:**

- Always handle all possible path patterns in the active tab detection logic
- Consider using a more generic approach that matches the base path of each tab
- Test the tab selection with all possible route combinations
- Remember to handle both root paths and nested paths for each section
- Keep the tab selection logic consistent across all sections of the application

60. **When handling CSV imports and data parsing:**

- Create proper interfaces for CSV data structures instead of using `any` type
- Import and use existing enums/types for fields that have predefined values
- Use TypeScript's type system to catch potential data mismatches early
- Consider using zod schemas for runtime validation of parsed data
- Make the expected data structure clear through types for better maintainability
- Use proper typing with Papa Parse's generic types for better type inference

61. **When using React Query with useEffect:**

- Wrap query keys in `useMemo` to prevent unnecessary re-renders
- Extract frequently used values (like IDs) into variables for better reusability
- Be consistent with dependency arrays across hooks
- Consider the performance implications of query key changes
- Use proper typing for query keys to catch potential issues early
- Remember that query keys are used for cache management and should be stable

62. **When working with Next.js 15 page props:**

- Use `Promise<T>` type for `params` and `searchParams` in page components
- Always await the params before accessing their properties
- Follow Next.js naming conventions (e.g., `PageProps` interface)
- Remember this is a breaking change from Next.js 14
- Consider creating reusable types for common param patterns
- Update all page components in the app to handle async params consistently
