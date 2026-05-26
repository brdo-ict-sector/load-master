# Product Roadmap

## Context

- **Launch model:** A single **full launch** of v1.0 to an initial group of **~5 users** (PMs + experts) — no separate pilot.
- **MVP shape:** A **thin slice of both pillars** (formal *and* actual load) end to end, with the **full view breadth** (weekly / monthly / yearly, in both tabular and graphical form) included in v1.0.
- **Sequencing:** Phases are **ordered by priority, without fixed dates**. Each phase lists its goal, the features it delivers, and a "Done when" definition. Phases 0–3 together constitute the **v1.0 full launch**; phases 4+ are fast-follow.

---

## Phase 0 — Foundation & Access

**Goal:** A logged-in user can reach the app securely over HTTPS, with roles enforced.

- Monorepo scaffold (`frontend/` React+Vite+TS, `backend/` NestJS+TS).
- PostgreSQL + Prisma schema baseline and migrations.
- VPS provisioning: Nginx reverse proxy, DuckDNS subdomain, Let's Encrypt HTTPS, systemd service.
- Authentication: admin-provisioned accounts, username/password (Argon2), server-side session cookies.
- Authorization: roles `Admin`, `PM`, `Expert` with route guards.
- CI/build from GitHub; deploy to VPS.

**Done when:** A user logs in over HTTPS on the DuckDNS domain; an Admin can create accounts; role-based access is enforced.

---

## Phase 1 — Project Profiles & Formal Load (PM)

**Goal:** A PM can plan a project's contracted capacity.

- Create/edit a **project profile**.
- Assign the **formally involved experts** to a project.
- Enter **formal load** per expert per month (days/month, on the 20-working-days/month basis).
- Underlying data model supporting week / month / year granularity for formal load.

**Done when:** A PM creates a project, assigns experts, and records each expert's contracted days.

---

## Phase 2 — Actual Load & Audit Trail (Expert)

**Goal:** Experts record reality, and every change is accountable.

- **Actual load** entry by experts (time really spent on tasks).
- **Audit trail:** append-only log capturing actor, timestamp, entity, action, and before/after values for all formal and actual load changes.
- Change history visible per entry (who changed what, when).

**Done when:** An expert records actual load; every formal/actual change is attributed to a user and timestamp and is viewable.

---

## Phase 3 — Views & Visualization (completes v1.0)

**Goal:** Both formal and actual capacity are visible across all horizons, in both formats.

- **Weekly / monthly / yearly** views for both formal and actual levels.
- **Tabular** and **graphical** (ECharts) presentation for each horizon.
- **Formal-vs-actual comparison** surfacing the gap (over-/under-load) per expert and per project.

**Done when:** All horizon × format combinations are available for both levels, and plan-vs-reality is visible at a glance. → **v1.0 full launch to ~5 users.**

---

## Phase 4 — Finance Export (fast-follow)

**Goal:** Finance gets clean numbers without chasing PMs.

- **XLSX export** of covered (paid) days matching the finance department's template.
- On-demand download plus the monthly **by-the-25th** schedule (NestJS scheduler).

**Done when:** A correct templated export of covered days can be produced for a given reporting month.

> **Trade-off note:** Finance export is an explicit stakeholder requirement tied to a monthly deadline (25th). It sits here because v1.0 is a thin slice. **If the first monthly reporting cycle falls before this phase ships, pull Phase 4 forward into v1.0.**

---

## Phase 5 — Change Analytics

**Goal:** Learn where plan and reality diverge.

- Analytics on **actual-load changes**, broken down **per project** and **per expert**.
- Comparison against the **formal baseline** (drift, trends over time).
- Tabular + graphical presentation, consistent with Phase 3.

**Done when:** A user can analyze actual-load change patterns per project and per expert against the formal plan.

---

## Phase 6 — Hardening & Operations

**Goal:** Run reliably for the team.

- Automated **PostgreSQL backups** + restore check.
- Admin UX for user management and account lifecycle.
- Logging/monitoring, error handling, and basic performance tuning.
- Accessibility and UX polish on tables/charts.

**Done when:** Backups are automated and verified, admins can self-serve user management, and the app is observably stable.

---

## Out of scope for now (revisit later)

- Email/SMTP features (self-service password reset, magic links, reminders).
- Self-service signup (accounts stay admin-provisioned).
- Paid custom domain (DuckDNS covers the initial launch).
- GitHub Pages hosting (static-only; cannot serve auth or the database).
