# Feature: Migrate the app to use Next.js v15 and React v19

Since Clerk needs to work for Nextjs v15 with React 19, we need to migrate the app to use Next.js v15 and React v19.

## Analysis

### 1. Core Dependencies Impact

Based on the package.json,

```json
    "next": "15.1.6",
    "next-themes": "^0.4.4",
    "react": "18.2.0",
    "react-day-picker": "8.10.1",
    "react-dom": "18.2.0",
```

IMPORTANT: DO NOT DOWNGRADE NEXT.JS VERSION (15.1.6 IS THE CORRECT VERSION) !!!

We need to update:

- react: 18.2.0 → 19.0.0
- react-dom: 18.2.0 → 19.0.0
- @types/react: 18.2.0 → 19.0.1

### 2. Breaking Changes Analysis

#### a. Server Components & Actions

The project heavily uses Server Components and Server Actions. React 19's changes to these features include:

- useFormState is replaced by useActionState
- Enhanced useFormStatus with additional properties
- All Server Actions need to be async in Next.js 15 + React 19

#### b. Component Impact

The following components will need attention:

1. Theme Provider:

```typescript
"use client"

import * as React from "react"
import { ThemeProvider as NextThemesProvider } from "next-themes"
import type { ThemeProviderProps } from "next-themes"

export function ThemeProvider({ children, ...props }: ThemeProviderProps) {
  return <NextThemesProvider {...props}>{children}</NextThemesProvider>
}
```

Needs verification for React 19 compatibility with next-themes. 2. Form Components:

```typescript
const FormMessage = React.forwardRef<
  HTMLParagraphElement,
  React.HTMLAttributes<HTMLParagraphElement>
>(({ className, children, ...props }, ref) => {
  const { error, formMessageId } = useFormField()
  const body = error ? String(error?.message) : children

  if (!body) {
    return null
  }

  return (
    <p
      ref={ref}
      id={formMessageId}
      className={cn("text-[0.8rem] font-medium text-destructive", className)}
      {...props}
    >
      {body}
    </p>
  )
})
FormMessage.displayName = "FormMessage"

export {
  useFormField,
  Form,
  FormItem,
  FormLabel,
  FormControl,
  FormDescription,
  FormMessage,
  FormField
}
```

Form handling components may need updates due to React 19's form handling changes. 3. Third-Party Dependencies Analysis

### 3. Critical packages to verify compatibility:

1. UI Components:

- @radix-ui/ packages (multiple components)
- shadcn/ui components
- react-hook-form

2. Data Visualization:

- recharts (for charts)

3. Maps Integration:

- @react-google-maps/api
- react-leaflet

### 4. Required Updates

TypeScript Configuration:

```json
{
  "compilerOptions": {
    "target": "ES2017",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

May need updates to support React 19 types.

ESLint Configuration:

```json
import { dirname } from "path";
import { fileURLToPath } from "url";
import { FlatCompat } from "@eslint/eslintrc";

const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);

const compat = new FlatCompat({
  baseDirectory: __dirname,
});

const eslintConfig = [
  ...compat.extends("next/core-web-vitals", "next/typescript"),
];

export default eslintConfig;
```

### 5. Potential Issues

1. Client Components:

- All "use client" components will need testing for React 19 hooks compatibility
- Form handling components may need updates
- Event handler patterns might need adjustments

3. Server Actions:

- Need to ensure all server actions are properly async
- Update error handling patterns for React 19 6.

### 6. Risk Assessment

Medium-High Risk:

- Form handling changes in React 19
- Server Actions async requirements
- Third-party component compatibility
- TypeScript type definitions updates

### 7. Migration Strategy Recommendation

1. Create a staging branch for the migration
2. Update core dependencies first:

```json
{
  "dependencies": {
    "next": "15.0.4",
    "react": "^19.0.0",
    "react-dom": "^19.0.0"
  },
  "devDependencies": {
    "@types/react": "^19.0.1",
    "@types/react-dom": "^19.0.1"
  }
}
```

3. Run type checking and fix TypeScript errors
4. Test all form submissions and server actions
5. Verify third-party component functionality
6. Update documentation and comments for React 19 patterns

## GOALS:

The goal is to migrate the app to use Next.js v15 and React v19 with versions detailed on the analysis section.

## REQUIREMENTS:

- Just focus on migrating the app to use Next.js v15 and React v19 with versions detailed on the analysis section. Do not tackle any other functionality.

## CONSTRAINTS:

- Do not install or run commands on the composer. Always ask me to install any dependency or run commands on the terminal
- Do not create or modify any other functionality, design or file other than the ones required to add the new functionality.

--- PROMPT ---

Lets migrate the version of React according to the analysis section. Lets tackle the migration process step by step and use the scratchpad to annotate your reasoning and progress, and to keep track of the tasks. Also use the scratchpad to write down any important lessons learned after the process.
