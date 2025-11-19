# Flute Portal Prototype — Tech Direction

This document defines the technical approach, architecture, and coding conventions for the Flute Portal Prototype.
It is written for AI coding assistants and multiple product managers to ensure consistent implementation across feature files.

---

## 1. Purpose

The prototype will:

* Demonstrate functional workflows for usability testing and stakeholder review.
* Support three personas: **Admin**, **Affiliate (ISO/ISV)**, and **Merchant**.
* Provide realistic navigation, CRUD interactions, search, filters, and role-based views.
* Enable fast iteration by product managers using AI assistants.

The prototype is **not** production code and intentionally avoids back-end infrastructure.

---

## 2. High-Level Architecture

The application is a **frontend-only, client-side web app** built with **Next.js** and deployed on **Vercel**.

There is:

* No real backend
* No real database
* No identity system

All state and “API calls” occur locally in the browser.

```
React (Next.js) → Fake API Layer → Zustand Stores → localStorage
```

This creates the illusion of:

* Asynchronous API calls
* CRUD capabilities
* Role-based access
* Merchant/affiliate/admin separation

without external dependencies.

---

## 3. Tech Stack

### 3.1 Core Technologies

* **Framework:** Next.js (App Router)
* **Language:** TypeScript
* **UI Library:** React (functional components only)

All pages and components related to the prototype behavior are **client components**.

At the top of each page or component that uses state, effects, or browser APIs, include:

```tsx
"use client";
```

### 3.2 State Management

Use **Zustand** for domain-specific state stores:

* `/src/state/merchantStore.ts`
* `/src/state/transactionStore.ts`
* `/src/state/affiliateStore.ts`
* `/src/state/userStore.ts`

Each store:

* Keeps data in memory.
* Persists changes to `localStorage`.
* Provides CRUD methods.
* Acts as the single source of truth for that domain.

### 3.3 Fake API Layer

Folder: `/src/api`

Each domain has a fake API module that exposes asynchronous functions which internally use the corresponding Zustand store.

Example for merchants:

```ts
// /src/api/merchants.ts
import { merchantsStore } from "../state/merchantStore";
import { delay } from "../utils/delay";

export async function listMerchants() {
  await delay(150);
  return merchantsStore.getAll();
}

export async function createMerchant(input: NewMerchant) {
  await delay(150);
  return merchantsStore.create(input);
}

export async function updateMerchant(id: string, patch: Partial<Merchant>) {
  await delay(150);
  return merchantsStore.update(id, patch);
}

export async function deleteMerchant(id: string) {
  await delay(150);
  return merchantsStore.remove(id);
}
```

Rules for the fake API layer:

* All functions return a `Promise`.
* Each call simulates latency using a shared `delay` utility.
* Fake APIs call into Zustand stores and never bypass them.
* UI components and pages **call the fake API layer**, not the stores directly.

This ensures a clean boundary that can be swapped for real HTTP APIs later.

### 3.4 Persistence

* All state changes persist to `localStorage`.
* Seed JSON files live under `/src/data/*.json`.
* On initial load, each store attempts to hydrate from `localStorage`. If no data exists, it loads seed data from the corresponding JSON file.
* A global **“Reset Demo Data”** action clears `localStorage` for the prototype keys and reloads the seed data.

This behavior enables repeatable usability tests and clean demo setups.

### 3.5 UI Libraries and Styling

* **Styling:** Tailwind CSS
* **Component primitives:** Radix UI or Headless UI for common patterns such as dialogs, menus, lists, and selects.
* **Icons:** Heroicons or Lucide icons.

Design principles:

* Clean and modern portal look.
* Consistent spacing and typography.
* Clear hierarchy between page title, section headings, tables, and actions.
* Accessible components (focus states, keyboard navigation, sensible aria attributes).

### 3.6 Role Switching

Define a global React context for role state.

```ts
type Role = "admin" | "affiliate" | "merchant";
```

Store this in `/src/context/RoleContext.tsx` and expose a hook such as `useRole()`.

The role switcher:

* Appears in the main app header.
* Allows switching between Admin, Affiliate, and Merchant.
* Updates global role state.

Each page enforces minimal access control based on the current role. For example:

```tsx
const { role } = useRole();

if (role !== "admin") {
  return <NotAuthorized />;
}
```

Navigation rendering also depends on the active role (see Navigation Model).

---

## 4. App Structure

Directory layout:

```
/src
  /app              # Next.js App Router pages
    /(portal)
      /dashboard
      /transactions
      /merchants
      /affiliates
      /admin
      layout.tsx
      page.tsx
  /components       # Shared UI components
  /api              # Fake API modules
  /state            # Zustand stores
  /context          # Role context
  /data             # Seed JSON
  /hooks            # Shared hooks
  /utils            # Utilities such as delay, localStorage helpers
  /design           # Design tokens (colors, spacing, typography)
/features           # Feature specs in markdown
```

Conventions:

* Use the App Router (`/app` directory) for routing.
* Group portal pages under a single segment such as `/(portal)` for clarity.
* Keep shared layout elements (header, nav, role switcher) in `layout.tsx`.

---

## 5. Coding Standards

### 5.1 Components

* Use React functional components exclusively.
* Prefer small, composable components over large monoliths.
* Co-locate components with their feature when appropriate; move to `/components` when reused.

### 5.2 Client Components

* Any component that uses hooks, browser APIs, or role context must start with:

```tsx
"use client";
```

* Layout and page components that rely on interactive behavior are client components.

### 5.3 TypeScript

* Define interfaces and types for all core entities:

  * `Merchant`
  * `Affiliate`
  * `Transaction`
  * `User`

* Place shared types in `/src/types`.

* All public functions in the fake API layer must be strongly typed.

### 5.4 Store Access

* UI components and pages call fake API modules rather than directly manipulating Zustand stores.
* Zustand stores are only imported in:

  * Their own definition files.
  * The fake API layer for that domain.

### 5.5 Business Logic

* Keep business logic inside:

  * Fake API functions.
  * Domain-specific helper functions.

* Page components should focus on:

  * Data fetching via fake APIs.
  * Mapping domain state to UI.
  * Handling user interactions and forwarding intent to the fake API.

---

## 6. Design System

Define simple design tokens in `/src/design/tokens.ts`.

Example structure:

```ts
export const colors = {
  primary: "#4F46E5",
  primarySoft: "#EEF2FF",
  accent: "#6366F1",
  accentSoft: "#E0F2FE",
  grayLight: "#F3F4F6",
  gray: "#9CA3AF",
  grayDark: "#111827",
  danger: "#DC2626",
  warning: "#F59E0B",
  success: "#16A34A",
};

export const spacing = {
  xs: 4,
  sm: 8,
  md: 16,
  lg: 24,
  xl: 32,
};

export const typography = {
  pageTitle: "text-2xl font-semibold",
  sectionTitle: "text-xl font-semibold",
  body: "text-sm text-gray-800",
  label: "text-xs font-medium text-gray-600",
};
```

Use these tokens through Tailwind utility classes and custom className helpers to maintain consistency.

---

## 7. CRUD Behavior Requirements

Each core entity must implement the following behaviors via the fake API layer and UI:

### 7.1 Create

* Use a modal or dedicated create form page.
* Perform basic client-side validation.
* On save, call the appropriate fake API `create` method.
* Update the UI list immediately after creation.

### 7.2 Read

* Provide a list screen with sorting and filtering as appropriate.
* Support simple search where meaningful (for example by merchant name or transaction ID).
* Detail views can be modals or separate pages depending on complexity.

### 7.3 Update

* Allow editing of key fields through a modal or edit page.
* On save, call the fake API `update` method.
* Reflect changes immediately in lists and details.

### 7.4 Delete

* Confirm destructive actions via a dialog.
* On confirm, call the fake API `delete` method.
* Remove the entity from visible lists.

### 7.5 Persistence

* All CRUD actions must cause the corresponding Zustand store to:

  * Update its in-memory data.
  * Persist to `localStorage`.

---

## 8. Navigation Model

Role determines available pages and navigation entries.

### 8.1 Merchant Role

* **Dashboard**
* **Transactions**
* **Settlements / Deposits**
* **Payment Configuration** (simplified settings)

### 8.2 Affiliate Role (ISO/ISV)

* **Portfolio Dashboard** (aggregated metrics across merchants)
* **Merchant List** (onboarding state, KYC status, enablement flags)
* **Rollup Reporting** (volume, trends, basic breakdowns)

### 8.3 Admin Role

* **User and Role Management** (assign roles, activate/deactivate users)
* **System Flags / Feature Toggles** (prototype switches such as enabling CNP, enabling webhooks, enabling multi-processor)
* **Data Controls** (access to Reset Demo Data tools)

The main navigation component reads the current role from `RoleContext` and displays only relevant items.

---

## 9. Workflow for PMs Using AI Assistants

1. Add or update a **feature spec markdown file** under `/features/` describing the user story, flows, and UI expectations.
2. Create a Git branch using the pattern:

   * `feature/<short-feature-name>`
3. Instruct the AI coding assistant to:

   * Read `TECH-DIRECTION.md`.
   * Read the specific feature spec file.
   * Implement or extend pages, components, and fake API functions following this document.
4. Run the app locally and perform a basic smoke test.
5. Open a Pull Request into `main`.
6. Use the Vercel preview URL for review and usability checks.

---

## 10. Out of Scope

The prototype intentionally excludes:

* Real backend services
* Authentication and identity management
* C# code
* Databases
* Server-side API routes in Next.js
* Real payment processing or gateway integrations
* Direct connections to Flute production systems

The focus is on **functional UX flows** and **portal behavior**, not production readiness.

---

## 11. Future Upgrade Path

After validating the prototype, the fake API layer can be replaced with real endpoints. Options include:

* C# APIs aligned with Flute production services.
* Mock Service Worker (MSW) for richer network simulation while keeping the same UI.

The UI structure, routing, and state usage should remain stable through that transition.

---

## 12. Summary

The Flute Portal Prototype is a Next.js and TypeScript client-side application with:

* Zustand for state management.
* localStorage-backed persistence.
* A fake API layer simulating async CRUD behaviors.
* A global role switcher controlling navigation and access.
* A PR-based workflow and Vercel deployments for fast iteration.

All implementation work by humans and AI assistants must align with this document.
