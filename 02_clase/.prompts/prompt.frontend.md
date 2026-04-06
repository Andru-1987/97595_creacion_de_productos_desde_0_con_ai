# SpaceDesk — MVP Prompt

## Overview

Build **SpaceDesk**, a multi-tenant SaaS for coworking space management. Each tenant is identified by a slug in the URL (e.g., `/t/palermo-cowork`). The app is a fully functional PWA with responsive design, using mock data only. No real database or external APIs.

## Stack (Fixed)

- **Framework:** Next.js 14 (App Router)
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **UI Components:** shadcn/ui
- **Icons:** lucide-react
- **Charts:** Recharts
- **State Management:** Zustand
- **Forms:** React Hook Form + Zod
- **Dates:** date-fns
- **Toasts:** sonner
- **PWA:** next-pwa (with manifest.json)

All data comes from a single `src/data/mockData.json` file. No axios, Redux, or real auth.

## Architecture

- **Public routes:** `/login`
- **Protected routes:** `/t/[tenantSlug]/...` (requires authentication)
- **Layout:** Sidebar (collapsible) + Header for admin views; top nav for member portal.
- **Responsive:** Mobile drawer for sidebar, bottom navigation bar for admin on mobile.

## Roles & Access

| Role     | Access                                    |
|----------|-------------------------------------------|
| owner    | Full admin panel (all modules)            |
| admin    | Admin panel except tenant settings        |
| member   | Only `/portal` (self‑service)             |

Mock login: credentials shown on login page (`owner@palermo.com` / `demo1234`, etc.). Authentication stored in Zustand + localStorage.

## Modules

### 1. Dashboard (`/dashboard`)

- **Stats cards:** active members, today’s reservations, monthly occupancy %, pending payments.
- **Occupancy chart:** area chart for last 30 days (room/desk/office occupancy %).
- **Recent reservations:** table with member, space, time, status.

### 2. Reservations (`/reservas`)

- Calendar view (weekly) with time slots and space selector.
- List view with filters (status, space, date range).
- New reservation form with conflict validation.
- Member can only book for themselves; admin/owner can book for any member.

### 3. Spaces (`/espacios`)

- Grid of spaces with type, capacity, pricing, status.
- Owner can add/edit/delete spaces; admin read‑only.
- Occupancy drawer for each space.

### 4. Members (`/miembros`)

- Table of members with filters and search.
- Member detail page: plan details, reservation history, payment history.
- Admin/owner can edit, suspend, or renew membership.

### 5. Memberships (`/membresias`) — owner only

- Manage plans: flexible desk, fixed desk, private office.
- Pricing, room credits, access hours.

### 6. Billing (`/facturacion`)

- Monthly invoices table with status (paid/pending/overdue).
- Summary: total billed, pending, members in arrears.
- Mark invoices as paid (admin/owner).

### 7. Member Portal (`/portal`)

- For members only.
- Shows current plan, usage of room credits, upcoming reservations.
- New reservation form (only for self) with availability check.

## Mock Data Requirements

`src/data/mockData.json` must contain:

- **Tenants:** 2 (e.g., palermo-cowork, rosario-hub)
- **Users:** per tenant: 1 owner, 1 admin, 4 members (12 total, passwords plain text for mock)
- **Spaces:** per tenant: 2 meeting rooms, 4 desks, 1 office
- **Plans:** per tenant: 3 plans (Flexible, Fixed Desk, Private Office)
- **Members:** 4 per tenant, each with a membership (mix of active, expired, suspended)
- **Reservations:** 30 per tenant, spanning last 14 days and next 7 days, various statuses
- **Invoices:** per member: last two months, mixed payment statuses

A service layer (`src/lib/mockService.ts`) should provide CRUD‑like functions that operate on the in‑memory data (mutations are lost on reload, acceptable for MVP).

## Design & UX

- **Colors:** defined as CSS variables (dark blue primary, etc.)
- **Fonts:** Sora (titles) and DM Sans (body) via Google Fonts.
- **Components:** use shadcn/ui for buttons, cards, badges, tables, dialogs, etc.
- **States:** loading skeletons, toasts for success/error.
- **Responsive:** tables collapse to cards on mobile; calendar adapts to single day view.

## PWA

- Provide `manifest.json` and configure `next-pwa` in `next.config.js`.
- Icons: placeholder SVG icons (192x192, 512x512).

## Delivery

Generate the complete codebase with all files, structured as per Next.js conventions. Include the `mockData.json`, all types, stores, components, and pages. Ensure the app runs with `npm run dev` after installing dependencies. The generated output should be self‑contained and require no manual adjustments.

**Expected output:** All source files with paths, plus installation instructions (npm commands). No placeholder comments; fully functional code.