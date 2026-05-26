# Tech Stack

## Architecture at a glance

A single full-stack TypeScript application, served from **one origin on the VPS** (no GitHub Pages, no CORS). Nginx terminates HTTPS and reverse-proxies to a Node API; the API serves both the JSON endpoints and the built static frontend. Data lives in PostgreSQL on the same VPS.

```
Browser ──HTTPS──> Nginx (DuckDNS subdomain, Let's Encrypt)
                     │
                     ├── /            → static React build
                     └── /api/*       → NestJS (Node) API
                                          │
                                          └── PostgreSQL
```

## Hosting & Infrastructure

- **Host:** Existing VPS (single origin — frontend + API + DB together).
- **Domain:** Free **DuckDNS** subdomain (e.g. `expert-load.duckdns.org`); repointable to a paid domain later with no app changes.
- **TLS/HTTPS:** Let's Encrypt via Certbot (auto-renewing).
- **Reverse proxy:** Nginx (HTTPS termination, static file serving, proxy to the API).
- **Process management:** systemd service (or PM2) for the Node process; PostgreSQL as a system service.
- **Code repo & CI:** GitHub (source of truth + CI/build). GitHub Pages is intentionally not used — it is static-only and cannot host the login or database.

## Backend

- **Runtime:** Node.js (LTS).
- **Language:** TypeScript.
- **Framework:** **NestJS** — modular structure, built-in auth **guards + role-based access control**, request validation (class-validator), and a built-in **scheduler** (`@nestjs/schedule`) for the monthly finance-export job.
- **ORM:** **Prisma** — type-safe data access and versioned migrations.
- **API style:** REST (JSON) under `/api`.

## Database

- **Engine:** **PostgreSQL**.
- **Why:** Reliable concurrent writes (multiple experts editing actual load at once), strong support for the weekly/monthly/yearly **aggregations**, and a durable relational **audit trail**.
- **Audit trail:** Dedicated append-only audit table capturing actor (user id), timestamp, entity, action, and before/after values for every change to formal and actual load.

## Frontend

- **Framework:** **React** + **TypeScript**, bundled with **Vite**.
- **Data fetching/cache:** **TanStack Query**.
- **Tables:** **TanStack Table** (headless data grid) for the tabular formal/actual views.
- **Charts:** **Apache ECharts** for the graphical weekly/monthly/yearly views.
- **Styling/UI:** Tailwind CSS + a lightweight component layer (e.g. shadcn/ui or Mantine) — final pick during setup.
- **Routing:** React Router.

## Authentication & Authorization

- **Model:** Admin-provisioned accounts (no self-service signup, no email/SMTP required).
- **Login:** Username/email + password.
- **Sessions:** Server-side **session cookies** — `httpOnly`, `Secure`, `SameSite=Lax`. Chosen over JWT because the app is same-origin; simpler and safer in the browser.
- **Password hashing:** **Argon2** (bcrypt acceptable fallback).
- **Roles:** `Admin` (manages users), `PM` (creates projects, sets formal load), `Expert` (records actual load). Enforced via NestJS role guards.
- **Email:** None required now. If self-service reset / magic links / reminders are added later, integrate a free transactional provider (e.g. Brevo) rather than sending mail from the VPS.

## Reporting & Export

- **Finance export:** Generated as **XLSX** (via `exceljs`) to match the finance department's template; downloadable on demand and on the monthly **by-the-25th** cadence.
- **Scheduling:** NestJS scheduler (cron) drives the monthly export/reminder.

## Tooling & Conventions

- **Package manager:** pnpm (or npm).
- **Lint/format:** ESLint + Prettier.
- **Testing:** Vitest (unit) + Supertest/Nest testing utilities (API); Playwright optional for E2E.
- **Monorepo layout:** Single repo with `frontend/` and `backend/` (shared types package optional).

## Explicitly deferred / not used

- **GitHub Pages** — static-only; cannot serve auth or the database.
- **Email/SMTP** — out of scope for v1 (admin-provisioned auth).
- **Paid custom domain** — optional later; DuckDNS covers v1 for free.
