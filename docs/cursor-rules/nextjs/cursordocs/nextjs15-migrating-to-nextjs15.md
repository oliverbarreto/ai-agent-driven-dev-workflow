# NextJS 15

## Upgrading NextJS from 14 to 15

To update to Next.js version 15, you can use the upgrade codemod:

```bash
npx @next/codemod@canary upgrade latest
```

If you prefer to do it manually, ensure that you're installing the latest Next & React versions:

```bash
npm i next@latest react@latest react-dom@latest eslint-config-next@latest
```

> Good to know: If you see a peer dependencies warning, you may need to update react and react-dom to the suggested versions, or you use the --force or --legacy-peer-deps flag to ignore the warning. This won't be necessary once both Next.js 15 and React 19 are stable.

## React 19

- The minimum versions of react and react-dom is now 19.
- useFormState has been replaced by useActionState. The useFormState hook is still available in React 19, but it is deprecated and will be removed in a future release. useActionState is recommended and includes additional properties like reading the pending state directly. Learn more.
- useFormStatus now includes additional keys like data, method, and action. If you are not using React 19, only the pending key is available. Learn more.
- Read more in the [React 19 upgrade guide](https://react.dev/blog/2022/03/08/react-18-upgrade-guide).

> Good to know: If you are using TypeScript, ensure you also upgrade @types/react and @types/react-dom to their latest versions.

## Async Request APIs (Breaking change)

Previously synchronous Dynamic APIs that rely on runtime information are now asynchronous:

- cookies
- headers
- draftMode
- params in layout.js, page.js, route.js, default.js, opengraph-image, twitter-image, icon, and apple-icon.
- searchParams in page.js

To ease the burden of migration, a codemod is available to automate the process and the APIs can temporarily be accessed synchronously.

### cookies

#### Recommended Async Usage

```ts
import { cookies } from "next/headers"

// Before
const cookieStore = cookies()
const token = cookieStore.get("token")

// After
const cookieStore = await cookies()
const token = cookieStore.get("token")
```

#### Temporary Synchronous Usage

```ts
// app/page.tsx
TypeScript

import { cookies, type UnsafeUnwrappedCookies } from "next/headers"

// Before
const cookieStore = cookies()
const token = cookieStore.get("token")

// After
const cookieStore = cookies() as unknown as UnsafeUnwrappedCookies
// will log a warning in dev
const token = cookieStore.get("token")
```

### headers

#### Recommended Async Usage

```typescript
import { headers } from "next/headers"

// Before
const headersList = headers()
const userAgent = headersList.get("user-agent")

// After
const headersList = await headers()
const userAgent = headersList.get("user-agent")
```

#### Temporary Synchronous Usage

```typescript
// app/page.tsx

import { headers, type UnsafeUnwrappedHeaders } from "next/headers"

// Before
const headersList = headers()
const userAgent = headersList.get("user-agent")

// After
const headersList = headers() as unknown as UnsafeUnwrappedHeaders
// will log a warning in dev
const userAgent = headersList.get("user-agent")
```

### draftMode

#### Recommended Async Usage

```typescript
import { draftMode } from "next/headers"

// Before
const { isEnabled } = draftMode()

// After
const { isEnabled } = await draftMode()
```

#### Temporary Synchronous Usage

```typescript
// app/page.tsx

import { draftMode, type UnsafeUnwrappedDraftMode } from "next/headers"

// Before
const { isEnabled } = draftMode()

// After
// will log a warning in dev
const { isEnabled } = draftMode() as unknown as UnsafeUnwrappedDraftMode
```

### params & searchParams

#### Asynchronous Layout

```typescript
// app/layout.tsx

// Before
type Params = { slug: string }

export function generateMetadata({ params }: { params: Params }) {
  const { slug } = params
}

export default async function Layout({
  children,
  params
}: {
  children: React.ReactNode
  params: Params
}) {
  const { slug } = params
}

// After
type Params = Promise<{ slug: string }>

export async function generateMetadata({ params }: { params: Params }) {
  const { slug } = await params
}

export default async function Layout({
  children,
  params
}: {
  children: React.ReactNode
  params: Params
}) {
  const { slug } = await params
}
```

#### Synchronous Layout

```typescript
// app/layout.tsx

// Before
type Params = { slug: string }

export default function Layout({
  children,
  params
}: {
  children: React.ReactNode
  params: Params
}) {
  const { slug } = params
}

// After
import { use } from "react"

type Params = Promise<{ slug: string }>

export default function Layout(props: {
  children: React.ReactNode
  params: Params
}) {
  const params = use(props.params)
  const slug = params.slug
}
```

#### Asynchronous Page

```typescript
// app/page.tsx

// Before
type Params = { slug: string }
type SearchParams = { [key: string]: string | string[] | undefined }

export function generateMetadata({
  params,
  searchParams
}: {
  params: Params
  searchParams: SearchParams
}) {
  const { slug } = params
  const { query } = searchParams
}

export default async function Page({
  params,
  searchParams
}: {
  params: Params
  searchParams: SearchParams
}) {
  const { slug } = params
  const { query } = searchParams
}

// After
type Params = Promise<{ slug: string }>
type SearchParams = Promise<{ [key: string]: string | string[] | undefined }>

export async function generateMetadata(props: {
  params: Params
  searchParams: SearchParams
}) {
  const params = await props.params
  const searchParams = await props.searchParams
  const slug = params.slug
  const query = searchParams.query
}

export default async function Page(props: {
  params: Params
  searchParams: SearchParams
}) {
  const params = await props.params
  const searchParams = await props.searchParams
  const slug = params.slug
  const query = searchParams.query
}
```

#### Synchronous Page

```typescript
// app/page.tsx

"use client"

// Before
type Params = { slug: string }
type SearchParams = { [key: string]: string | string[] | undefined }

export default function Page({
  params,
  searchParams
}: {
  params: Params
  searchParams: SearchParams
}) {
  const { slug } = params
  const { query } = searchParams
}

// After
import { use } from "react"

type Params = Promise<{ slug: string }>
type SearchParams = Promise<{ [key: string]: string | string[] | undefined }>

export default function Page(props: {
  params: Params
  searchParams: SearchParams
}) {
  const params = use(props.params)
  const searchParams = use(props.searchParams)
  const slug = params.slug
  const query = searchParams.query
}
```

```typescript
// app/page.tsx

// Before
export default function Page({ params, searchParams }) {
  const { slug } = params
  const { query } = searchParams
}

// After
import { use } from "react"

export default function Page(props) {
  const params = use(props.params)
  const searchParams = use(props.searchParams)
  const slug = params.slug
  const query = searchParams.query
}
```

### Route Handlers

```typescript
// app/api/route.ts

// Before
type Params = { slug: string }

export async function GET(request: Request, segmentData: { params: Params }) {
  const params = segmentData.params
  const slug = params.slug
}

// After
type Params = Promise<{ slug: string }>

export async function GET(request: Request, segmentData: { params: Params }) {
  const params = await segmentData.params
  const slug = params.slug
}
```

```typescript
// app/api/route.ts

// Before
export async function GET(request, segmentData) {
  const params = segmentData.params
  const slug = params.slug
}

// After
export async function GET(request, segmentData) {
  const params = await segmentData.params
  const slug = params.slug
}
```

### runtime configuration (Breaking change)

The runtime segment configuration previously supported a value of experimental-edge in addition to edge. Both configurations refer to the same thing, and to simplify the options, we will now error if experimental-edge is used. To fix this, update your runtime configuration to edge. A codemod is available to automatically do this.

#### fetch requests

fetch requests are no longer cached by default.

To opt specific fetch requests into caching, you can pass the cache: 'force-cache' option.

```typescript
// app/layout.js

export default async function RootLayout() {
  const a = await fetch("https://...") // Not Cached
  const b = await fetch("https://...", { cache: "force-cache" }) // Cached

  // ...
}
```

To opt all fetch requests in a layout or page into caching, you can use the export const fetchCache = 'default-cache' segment config option. If individual fetch requests specify a cache option, that will be used instead.

```typescript
// app/layout.js

// Since this is the root layout, all fetch requests in the app
// that don't set their own cache option will be cached.
export const fetchCache = "default-cache"

export default async function RootLayout() {
  const a = await fetch("https://...") // Cached
  const b = await fetch("https://...", { cache: "no-store" }) // Not cached

  // ...
}
```

### Route Handlers

GET functions in Route Handlers are no longer cached by default. To opt GET methods into caching, you can use a route config option such as export const dynamic = 'force-static' in your Route Handler file.

```typescript
// app/api/route.js

export const dynamic = "force-static"

export async function GET() {}
```

### Client-side Router Cache

When navigating between pages via <Link> or useRouter, page segments are no longer reused from the client-side router cache. However, they are still reused during browser backward and forward navigation and for shared layouts.

To opt page segments into caching, you can use the staleTimes config option:

```typescript
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    staleTimes: {
      dynamic: 30,
      static: 180
    }
  }
}

module.exports = nextConfig
```

Layouts and loading states are still cached and reused on navigation.

### next/font

The @next/font package has been removed in favor of the built-in next/font. A codemod is available to safely and automatically rename your imports.

```typescript
app / layout.js

// Before
import { Inter } from "@next/font/google"

// After
import { Inter } from "next/font/google"
```

### bundlePagesRouterDependencies

experimental.bundlePagesExternals is now stable and renamed to bundlePagesRouterDependencies.

```typescript
// next.config.js

/** @type {import('next').NextConfig} */
const nextConfig = {
  // Before
  experimental: {
    bundlePagesExternals: true
  },

  // After
  bundlePagesRouterDependencies: true
}

module.exports = nextConfig
```

### serverExternalPackages

experimental.serverComponentsExternalPackages is now stable and renamed to serverExternalPackages.

```typescript
// next.config.js

;/\*_ @type {import('next').NextConfig} _/
const nextConfig = {
  // Before
  experimental: {
    serverComponentsExternalPackages: ["package-name"]
  },

  // After
  serverExternalPackages: ["package-name"]
}

module.exports = nextConfig
```

### Speed Insights

Auto instrumentation for Speed Insights was removed in Next.js 15.

To continue using Speed Insights, follow the Vercel Speed Insights Quickstart guide.

### NextRequest Geolocation

The geo and ip properties on NextRequest have been removed as these values are provided by your hosting provider. A codemod is available to automate this migration.

If you are using Vercel, you can alternatively use the geolocation and ipAddress functions from @vercel/functions instead:

```typescript
// middleware.ts

import { geolocation } from "@vercel/functions"
import type { NextRequest } from "next/server"

export function middleware(request: NextRequest) {
  const { city } = geolocation(request)

  // ...
}
```

```typescript
// middleware.ts

import { ipAddress } from "@vercel/functions"
import type { NextRequest } from "next/server"

export function middleware(request: NextRequest) {
  const ip = ipAddress(request)

  // ...
}
```
