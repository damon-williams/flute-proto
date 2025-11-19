
---

### `FEATURE-TEMPLATE.md`

```markdown
# Feature Spec Template — Flute Prototype (MMS + POS)

> Copy this file to `/features/FEATURE-XX-<short-name>.md` and fill in all sections.  
> This template is designed to be consumed by AI coding assistants together with `FLUTE.md` and `TECH-DIRECTION.md` to generate feature implementations.

---

## 1. Feature Metadata

- **Feature ID:** `FEATURE-XX-<SHORT-NAME>`
- **Title:** One-line human-readable title
- **App Context:** `MMS` | `POS` | `Shared`
- **Primary Role(s):**
  - MMS roles: `Admin` | `Affiliate` | `Merchant`
  - POS roles: `Owner` | `Manager` | `Service Provider` | `Assistant`
- **Section of App:** (for example: MMS → Transactions, POS → Checkout, etc.)
- **Status:** (Draft / In Refinement / Approved)

---

## 2. Summary

A short paragraph (3–5 sentences) describing:

- What this feature does
- Who it is for
- Why it exists (business value)

Keep it high-level and non-technical.

---

## 3. Goals and Non-Goals

### 3.1 Goals

List 3–5 bullet points describing what success looks like, e.g.:

- Merchants can quickly locate a specific transaction by ID or date range (MMS).
- Service Providers can quickly take payment after a service is completed (POS).

### 3.2 Non-Goals

List explicit things not in scope for this feature, e.g.:

- No export to CSV in this iteration.
- No POS hardware integration.
- No advanced risk flags or chargeback workflows.

---

## 4. Personas, Roles, and App Context

Describe who uses this feature and in which app.

- **App Context:** MMS, POS, or Shared
- **Primary Role(s):** Who uses this most?
- **Secondary Role(s):** Who might view but not own it?
- **Access Rules:** Are any roles explicitly excluded?

Examples:

- **MMS Feature Example**  
  - App Context: MMS  
  - Primary: Merchant  
  - Secondary: Admin (read-only)  
  - Access: Only Merchant and Admin roles can access this page; Affiliates cannot.

- **POS Feature Example**  
  - App Context: POS  
  - Primary: Service Provider  
  - Secondary: Manager, Owner  
  - Access: Assistants can see a subset of controls; Service Providers cannot see configuration.

---

## 5. User Flows

Describe the main flows as numbered steps. Keep each flow tight and concrete.

### 5.1 Primary Flow

> Example (MMS): Merchant locates a transaction and issues a refund.  
> Example (POS): Service Provider completes a checkout after a haircut.

1. User selects appropriate **App Context** and **Role** via the Switcher.
2. User navigates to the relevant section (e.g., Transactions, Checkout).
3. User performs key actions as required by the flow.
4. User sees clear confirmation and updated state.

### 5.2 Secondary Flows

Add additional flows (view-only, edge cases, admin overrides, etc.) as needed.

---

## 6. UX and UI Requirements

Describe the shape of the UI without being overly prescriptive.

Include:

- Page-level layout (header, filters, table, list, form, etc.)
- Key components (tables, modals, forms, tabs, drawers)
- Important labels and terminology
- Sorting and filtering expectations

You may reference example layouts, such as:

- “A table with sticky header and pagination at the bottom” (MMS).
- “A simple POS-style checkout screen with big buttons for actions” (POS).

If helpful, include rough text-only wireframes.

---

## 7. Data Model for This Feature

Describe the entities and fields used by this feature from the perspective of the UI.

For each main entity, list:

- **Entity Name** (e.g., Transaction, POS Order)
- **Key Fields** displayed or edited:
  - `fieldName` — description (type if important)

Example (MMS):

- **Transaction**
  - `transactionId` — unique identifier
  - `createdAt` — date/time of authorization
  - `amount` — transaction amount
  - `status` — approved | declined | refunded | voided

Example (POS):

- **PosTicket**
  - `id` — unique identifier
  - `serviceDescription` — text describing the service
  - `amount` — ticket amount
  - `staffRole` — Owner | Manager | Service Provider | Assistant (for display)

Use realistic naming consistent with `FLUTE.md`.

---

## 8. Behaviors and Rules

Capture important behavior and validation rules. Examples:

- Which statuses allow which actions (e.g., only approved transactions can be refunded).
- Role-based behavior differences (e.g., Service Providers can take payment but not adjust tax settings).
- What happens after a successful action (UI feedback, state updates).
- How filters combine (AND/OR logic, default ranges).
- Any limits or truncation (e.g., max 100 records per page).

Be explicit about:

- What should happen
- When it should happen

Keep rules simple and prototype-friendly.

---

## 9. Fake API Requirements

Specify what the fake API layer needs to support for this feature.

For each operation, define:

- Function name
- Input parameters
- Expected behavior
- Return shape at a high level

Example:

- `listTransactions(params)` (MMS)
  - Inputs: filters (date range, status, search term)
  - Behavior: returns an array of matching transactions

- `createPosTicket(input)` (POS)
  - Inputs: basic ticket data (service, amount, staff)
  - Behavior: creates a POS ticket and returns it

You do not need to specify the full TypeScript signature, just clear intent.

---

## 10. UI States

Describe important UI states to handle:

- **Loading:** What should the user see while data is loading?
- **Empty:** What if there is no data yet?
- **Error:** What message or fallback should appear if something fails?
- **Success / Confirmation:** What acknowledgment is shown after an action?

Use concise descriptions, e.g.:

- “Show a skeleton table while loading” (MMS).
- “Show a simple empty state with a big ‘Start checkout’ button” (POS).

---

## 11. Analytics / Observability (Prototype Level)

For the prototype, analytics are conceptual only. If helpful, list the key events that would matter in production, such as:

- “User viewed Transactions page (MMS)”
- “User started Checkout (POS)”
- “User submitted refund”
- “User completed POS payment”

This informs naming and button placement, even if no real tracking is implemented.

---

## 12. Acceptance Criteria / Test Scenarios

List specific scenarios that must be supported in the prototype.

Write them as simple, concrete checks. Example:

1. A Merchant (MMS) can locate a transaction from yesterday by amount and last 4 digits.
2. A Merchant (MMS) can refund an approved transaction and see the status update to `refunded`.
3. A Service Provider (POS) can start a checkout, enter an amount, and see the payment appear in history after “completion”.
4. An Affiliate (MMS) cannot access POS routes.
5. App context and role changes via the Switcher correctly affect navigation and available actions.

These should be easy for a human tester to verify in the Vercel preview.

---

## 13. Open Questions / TBD

List items that are not yet decided but should not block initial implementation.

Examples:

- “Exact fee breakdown for settlements”
- “Exact POS tax handling behavior”

Where possible, propose a temporary assumption the implementation can use.

---

## 14. Notes for the AI Assistant

Use this section to provide additional guidance to the AI coding assistant.

Examples:

- “Prioritize readability over optimization.”
- “For POS, keep the layout touch-friendly with large hit targets.”
- “Reuse existing MMS components where it makes sense, but it’s OK for POS to feel slightly more ‘front-of-house’.”

This is free-form and optional, but often useful.
