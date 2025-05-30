---
description: Project Structure, Technology stack and developer guidelines
globs: *.tsx, *.ts, src/config/**/*.json
---
# Project Structure and Technology Stack of the project

## Project management

Please use the process described in [project-management.md](mdc:cursordocs/project-management.md) to utilize the `cursordocs/scratchpad.md` tool to keep track of implementation plans of main tasks, reflect progress, and lessons learned.

## Objective

The goal is to create a SaaS application to offer multiple clients (organizations) a solution for time tracking employee clock-in management.

## Technology stack

This project should use this technology stack:

- NextJS 15: with App router and `src` folder. It should use Server Components, Server Acctions and Server Side Rendering over API routes when possible. Use API routes for webhooks (eg: Clerk and Stripe).
- For styling it will use Tailwind CSS, Shadcn, Lucide Icons,
- For database it will use Neon Postgres Service (https://neon.tech/). Remember that Neon http driver does not allow transactions, so you need to instead perform the operations sequentially, and handle errors properly 
- It will use Drizzle as ORM,
- Zod for validation,
- Validate Forms with Zod and React-Hook-Form,
- Zustand for state management,
- Clerk for authentication,
- TanStack React Query for data fetching for pagination,
- Please DO NOT USE sonner for TOAST messages. Always USE SHADCN TOAST components.
- For infrastructure it will be deployed on Vercel.

## Project Structure and Environment

This is a Next.js application with App Router structure. 

The structure follows a clean architecture pattern with clear separation of concerns between UI components, business logic, and data access layers.

Here's a brief overview of the main directories:

1. `app/`: Contains all the routes and pages using Next.js 13+ App Router
- `(app)/`: Main application routes
    - `(app)/admin`: Main application routes for users with admin role
    - `(app)/users`: Main application routes for users
    - `(app)/auth`: Main application routes for auth

- `(marketing)/`: Marketing/public pages
- `actions/`: Server actions
- `api/`: API routes

2. `components/`: Shared components
- `ui/`: Shadcn UI components
- Other component categories (avatar, dialogs, navigation, etc.)

3. `db/`: Database configuration and schema
4. `hooks/`: Custom React hooks

5. `lib/`: Utility functions and services
- `services/`: Business logic services
- Various utility files

6. `types/`: TypeScript type and interfaces definitions

7. Use `dotenv` for environment variable management.
8. Follow patterns for environment-specific configurations in `eas.json` and `next.config.js`.

For the current folder structure run for example `tree src cursordocs  -L 9 -I "nodes_modules"`

# Developer Guidelines

## Code Style:

- Allways add comments to functions to explain what they do
- Write concise, readable TypeScript code
- Use functional and declarative programming patterns
- Follow DRY (Don't Repeat Yourself) principle
- Implement early returns for better readability
- Structure components logically: exports, subcomponents, helpers, types
- Prefer iteration and modularization over code duplication.
- Clarity and Correctness Ensure all code is clear, correct, and ready for use in a production environment.

## Naming Conventions

- Use descriptive variable names with auxiliary verbs (e.g., `isLoading`, `hasError`).
- Prefix event handlers with "handle" (handleClick, handleSubmit)
- Structure files with exported components, subcomponents, helpers, static content, and types.
- Use lowercase with dashes for directories (`components/users-table`)
- Favor named exports for components
- Ensure code is clean, well-documented, and follows the project's coding standards.
- Use descriptive and meaningful commit messages.

### Follow Official Documentation

- Adhere to the official documentation for each technology used.
- Stay updated with the latest best practices and updates, especially for Nextjs.
- We use Nextjs 15 and React 19, so for Nextjs, check the new breaking changes and focus on data fetching methods and routing conventions.

## TypeScript Usage

- Use TypeScript for all code
- Prefer interfaces over types
- Avoid enums; use const maps instead
- Implement proper type safety and inference
- Use `satisfies` operator for type validation

## Error Handling and Validation

- Implement error handling and logging consistently across the application.
- Implement proper error logging and user-friendly error messages.
- Prioritize error handling and edge cases.
- Handle errors and edge cases at the beginning of functions.
- Use early returns for error conditions to avoid deep nesting.
- Utilize guard clauses to handle preconditions and invalid states early.
- Use custom error types or factories for consistent error handling.

### UI and Styling

- Always use Shadcn for UI components.
- Utilize Shadcn theming capabilities for consistent design across platforms.
- Implement responsive design with a mobile-first approach.
- Ensure styling consistency between web and native applications.
- Always use Shadcn Toast notifications for important events.

## Performance Optimization

- Optimize for both web and mobile performance.
- Use dynamic imports for code splitting in Next.js.
- Implement lazy loading for non-critical components.
- Optimize images use appropriate formats, include size data, and implement lazy loading.

# Nextjs 15 and React 19 Best Practices & Breaking Changes

For more detailed documentation on how to migrate old Nextjs code to the new Nextjs features, reffer to [nextjs15-migrating-to-nextjs15.md](mdc:cursordocs/nextjs15-migrating-to-nextjs15.md) specially on how to use the new aysnc request APIs which is a breaking change from Nextjs v14.

### Component Architecture

- Favor React Server Components (RSC) where possible
- Use app router instead of old routing system
- Minimize 'use client' directives
- Implement proper error boundaries
- Use Suspense for async operations
- Optimize for performance and Web Vitals

### State Management

- Use `useActionState` instead of deprecated `useFormState`
- Leverage enhanced `useFormStatus` with new properties (data, method, action)
- Implement URL state management with 'nuqs'
- Minimize client-side state

### Async Request APIs (Breaking change)

Previously synchronous Dynamic APIs that rely on runtime information are now asynchronous:

- cookies
- headers
- draftMode
- params in layout.js, page.js, route.js, default.js, opengraph-image, twitter-image, icon, and apple-icon.
- searchParams in page.js

To ease the burden of migration, a codemod is available to automate the process and the APIs can temporarily be accessed synchronously.


```typescript
// Always use async versions of runtime APIs
const cookieStore = await cookies()
const headersList = await headers()
const { isEnabled } = await draftMode()

// Handle async params in layouts/pages
const params = await props.params
const searchParams = await props.searchParams
```