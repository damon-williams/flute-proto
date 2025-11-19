# Flute Portal Prototype

This repository contains the **Flute Portal Prototype**, a fully client-side, interactive web application used to demonstrate functional workflows for merchants, affiliates (ISO/ISV), and administrators on the Flute payment platform.

The prototype is specifically designed for **usability testing**, **stakeholder demos**, and **rapid prototyping** by product managers using AI coding assistants. It intentionally avoids production infrastructure and is not intended for deployment to customers.

---

## Overview

The prototype simulates:

* Portal navigation and UI flows
* CRUD operations for core entities (merchants, transactions, affiliates, users)
* Role-based access control using a role switcher (Admin / Affiliate / Merchant)
* Basic reporting and list views
* Interactive configuration pages

This is a **frontend-only Next.js application** using local state and browser persistence to emulate a real portal.

---

## Tech Stack

* **Framework:** Next.js (App Router)
* **Language:** TypeScript
* **State Management:** Zustand
* **Persistence:** localStorage
* **Fake API Layer:** Custom modules simulating async CRUD behavior
* **Styling:** Tailwind CSS
* **Components:** Radix UI / Headless UI
* **Hosting:** Vercel

The prototype has **no backend, database, or authentication system**.

---

## Key Concepts

### Client-Only Architecture

All logic runs in the browser. API calls are simulated through a structured fake API layer that mimics asynchronous behavior.

```
Next.js (client components)
   → Fake API Layer
       → Zustand Stores
           → localStorage
```

### Role Switcher

Instead of login, a global role selector allows testers to switch between:

* Admin
* Affiliate (ISO/ISV)
* Merchant

Navigation and page access are determined by the active role.

### Resettable Demo Data

Seed data is loaded from `/src/data/*.json` and persisted to localStorage. A global "Reset Demo Data" tool rebuilds state from scratch.

---

## Repository Structure

```
/src
  /app                # Next.js App Router
    /(portal)
      /dashboard
      /transactions
      /merchants
      /affiliates
      /admin
      layout.tsx
      page.tsx
  /components          # Shared UI components
  /api                 # Fake API modules
  /state               # Zustand stores
  /context             # Role context provider
  /data                # Seed JSON
  /hooks               # Reusable hooks
  /utils               # Helpers (delay, storage, etc.)
  /design              # Design tokens
/features              # Feature specifications (markdown)
```

---

## How to Run Locally

### 1. Install dependencies

```
yarn install
```

or

```
npm install
```

### 2. Start the dev server

```
yarn dev
```

App will be served at:

```
http://localhost:3000
```

### 3. Using the Prototype

* Use the **Role Switcher** in the header to change roles.
* Navigate through portal sections to simulate workflows.
* Add/edit/delete records through the UI.
* Reset demo data if the UI state becomes inconsistent.

---

## Contributing (For PMs and AI Assistants)

### 1. Create or update a feature spec under `/features/`

Each spec should describe:

* User story
* Required UI components and pages
* Expected behaviors
* CRUD needs
* Role access patterns

### 2. Create a branch

```
feature/<feature-name>
```

### 3. Ask the AI assistant to implement

Provide the assistant with:

* The feature spec
* `TECH-DIRECTION.md`
* Relevant file paths

### 4. Submit a Pull Request

* Vercel will auto-deploy a preview environment.
* Validate UI and flows via the preview URL.

---

## Deployment

The prototype is deployed automatically via Vercel.

* **Every PR** → Preview deployment
* **Main branch** → Production deployment

No backend environment variables or infrastructure are required.

---

## Out of Scope

The prototype does **not** include:

* Real authentication or authorization
* Backend services
* Database or persistence beyond browser storage
* Payment processing or gateway integrations
* C# or production-aligned backend code
* Security-hardening or performance tuning

---

## Additional Documentation

See **TECH-DIRECTION.md** for:

* Architectural details
* Coding conventions
* State management guidelines
* API simulation rules
* UI and styling standards
* Role-based navigation model

---

## License

Internal use only. Not licensed for external distribution.

---

## Summary

The Flute Portal Prototype provides a fast, flexible environment for validating UX flows and demonstrating platform capabilities. It embraces client-side simplicity, rapid iteration, and AI-assisted development to accelerate product discovery and feedback.
