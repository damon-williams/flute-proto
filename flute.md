# Flute Platform — Business & Product Context

This document provides **high-level business context** for the Flute platform. It is intentionally concise and written for **AI coding assistants** to understand the domain well enough to:

- Interpret individual feature specifications
- Generate product-relevant UI and workflows
- Produce accurate prototype implementations
- Align behaviors and naming with the real-world payment platform concepts

This is **not** a full product strategy or comprehensive business plan. It is the minimum viable context needed to build feature prototypes.

---

## 1. What Is Flute?

**Flute** is a modern payments enablement platform supporting both card-present and card-not-present payment acceptance. Flute provides tools for merchants, affiliates (ISOs/ISVs), and internal administrators to manage payment activity, merchant portfolios, operational workflows, and configuration.

Flute is delivered through:
- An **API platform** for developers and integrators
- A **web-based portal** for operational and business users
- A **processing gateway** that connects to multiple processors

This prototype represents the **web portal** only.

---

## 2. Core User Personas

Flute serves three distinct roles, each with different responsibilities and access patterns.

### 2.1 Merchant
Merchants are the businesses accepting payments through Flute.

They use the portal to:
- View transactions, batches, and settlements
- Search, filter, and export payment activity
- Perform actions (refund, void, resend receipt)
- Configure payment settings (API keys, webhooks, CNP/CP modes)
- Monitor funding events and deposit schedules

### 2.2 Affiliate (ISO / ISV)
Affiliates are organizations that **sponsor, onboard, or manage a portfolio of merchants**.

They use the portal to:
- Manage their merchant portfolio
- View rollup reporting across merchants
- Monitor onboarding and activation statuses
- View aggregate payment volume, trends, and performance
- Understand portfolio composition (verticals, channels, etc.)

### 2.3 Admin
Admins are internal Flute employees.

They use the portal to:
- Manage user accounts and assign roles
- Support affiliates and merchants
- Enable or disable features and capabilities
- Access operational tools needed for support and troubleshooting
- Perform system-level configuration (prototype simulation only)

---

## 3. Core Concepts in the Flute Platform

The following domain concepts are central to how Flute operates.

### 3.1 Merchant
A business entity that accepts payments via Flute. Attributes commonly include:
- Merchant name and legal name
- Merchant ID
- Status (active, onboarding, suspended)
- Processing capabilities (CP/CNP)
- Settlement preferences
- Associated affiliate

### 3.2 Transaction
A payment event.

Common attributes:
- Transaction ID
- Amount
- Status (approved, declined, refunded, voided)
- Card brand, last 4 digits
- Date/time
- Merchant
- Payment method type (CP, CNP)
- Actions (refund, void)

### 3.3 Settlement / Deposit
The grouping of transactions that are funded to the merchant.
- Deposit date
- Batch totals
- Net amount
- Fees (prototype simplified)

### 3.4 Affiliate
An ISO, ISV, or partner entity that manages multiple merchants.
Common attributes:
- Affiliate name
- Affiliate ID
- Portfolio size
- Portfolio volume metrics

### 3.5 User
A person who accesses the portal.
- Name
- Role (merchant, affiliate, admin)
- Associated entity (merchant or affiliate)

In this prototype, users switch roles via a **role switcher**, with no authentication.

---

## 4. What the Portal Allows Users To Do

This prototype simulates the high-level capabilities of the Flute portal.

### 4.1 Merchant Capabilities
- View merchant dashboard (recent activity and KPIs)
- View transactions and run basic queries
- Refund or void eligible transactions
- View settlement/deposit history
- Manage basic configuration (API keys, webhook endpoints, processing modes)

### 4.2 Affiliate Capabilities
- View aggregate metrics across their merchant portfolio
- View merchant-level data and statuses
- Track onboarding and activation progress
- See rollup reporting for volume and trends

### 4.3 Admin Capabilities
- Manage users and assign their roles
- Enable/disable system features for simulation
- Access prototype-level tools such as resetting demo data
- View all merchants and affiliates

---

## 5. Business Themes & Value Propositions

Flute as a real-world platform is built around several product pillars. These guide naming, structure, and behaviors inside the prototype.

### 5.1 Omni-Channel Payment Enablement
Flute supports card-present, card-not-present, and mobile wallet transactions through a unified model.

### 5.2 Merchant & Partner Self-Service
The portal reduces dependency on support teams by enabling merchants and affiliates to:
- Configure settings independently
- View and export data
- Resolve basic issues (refunds, activations, etc.)

### 5.3 Portfolio Intelligence for Affiliates
Affiliates get insights into:
- Volume
- Growth trends
- Merchant health
- Channel composition

### 5.4 Operational Efficiency for Admins
Admins have a single place to:
- View system activity
- Support customers
- Manage internal configurations

---

## 6. Data Simplification for the Prototype

The real Flute platform contains hundreds of fields and deep integration logic. For the purposes of this prototype:

- Data structures are simplified
- Calculations (fees, batch totals, risk scores) are not real
- Lists and reports are generated from seed JSON and local mutations only
- No integrations exist with external processors, identity systems, or risk engines

The focus is **functional user flows**, not accurate financial modeling.

---

## 7. Prototype Behaviors to Maintain

Across all features, the prototype should:

- Feel coherent and consistent from a real user's perspective
- Use realistic naming aligned with payments industry standards
- Maintain role-based separation of access
- Allow believable CRUD operations and portal navigation
- Simulate workflows cleanly even with simplified data
- Avoid implying nonexistent backend systems

The goal is for testers to understand how Flute will work once fully built.

---

## 8. How the AI Assistant Should Use This Document

When generating or implementing a feature, the assistant should:

1. Use this document to understand the **domain and business meaning** of entities.
2. Use the specific feature's markdown file to understand **requirements and desired behaviors**.
3. Use `TECH-DIRECTION.md` to understand **how to implement** those behaviors.
4. Produce a clean, self-contained implementation aligned with:
   - Portal concepts
   - User roles
   - Entity semantics
   - Payments workflows

Together, the three documents provide:
- Business context (this file)
- Technical direction (`TECH-DIRECTION.md`)
- Feature-level requirements (`/features/*.md`)

This combination forms the complete **Product Requirements Prompt** for one-shot prototype generation.

---

## 9. Summary

Flute is a modern, omni-channel payments enablement platform serving merchants, affiliates, and internal administrators. The portal is the central operational and analytical interface for these users. This prototype focuses on simulating the user experience, data views, and workflows while avoiding real backend complexity.

This document provides the essential business context needed for accurate and realistic feature implementations within the prototype.
