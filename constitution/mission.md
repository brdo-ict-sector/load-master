# Product Mission

## Pitch

**Expert Capacity Manager** is a load-master tool that helps an analytics center plan and monitor its experts' workload across projects, by tracking both *formal* capacity (contracted days per project) and *actual* capacity (real time spent on tasks) — so no expert is silently overloaded, no paid day goes unaccounted for, and the finance department gets clean monthly numbers.

## Users

### Primary Customers

- **Analytics center management:** Needs a single source of truth for how the sector's experts are allocated and consumed across all projects.
- **Finance department:** Needs reliable figures on project-covered (paid) days, exported on a fixed monthly cadence.

### User Personas

**Project Manager (PM)** *(logs in)*
- **Role:** Owns one or more project profiles.
- **Responsibilities:** Creates a project, defines which experts are formally involved, and records each expert's contracted load (days per month, on a 20-working-day-per-month basis).
- **Pain today:** Formal allocations live in scattered spreadsheets with no consolidated view of whether an expert is over- or under-committed across projects.

**Expert** *(logs in)*
- **Role:** A specialist allocated to one or more projects.
- **Responsibilities:** Records their *actual* workload — the real time spent on tasks — so the formal plan can be compared against reality.
- **Pain today:** No simple, accountable place to log actual effort; discrepancies between plan and reality are invisible until they cause overload.

**Finance officer** *(consumes exports, does not log in)*
- **Role:** Plans and reconciles paid days.
- **Responsibilities:** Receives a templated data export of covered days, submitted by the 25th of the reporting month.
- **Pain today:** Manually chasing PMs for numbers and reassembling them into the reporting template.

## The Problem

### Capacity is invisible until it breaks

Expert workload is split between a **formal level** (days contracted to a project) and an **actual level** (time really spent). When these only live in disconnected Excel files, nobody can see in time that an expert is overloaded — or, conversely, that capacity is sitting free. There is no audit trail of who changed what and when.

**Our Solution:** A shared tool that captures both levels side by side, attributes every change to a user and timestamp, and surfaces over-/under-load across every project an expert touches.

### Paid days are hard to plan and report

Finance must plan project-covered days and submit a templated report by the 25th of each month. Reassembling this from spreadsheets is slow and error-prone.

**Our Solution:** Formal (contracted) days are first-class data, aggregated automatically and exportable to the finance template on schedule.

### Plan vs. reality is never analyzed

Without comparing contracted days against actual time, the organization can't learn where estimates drift or which projects consistently consume more than planned.

**Our Solution:** Analytics on actual-workload changes, viewable per project and per expert, against the formal baseline.

## Differentiators

### Two levels, one view
Unlike a spreadsheet that tracks either a plan *or* a timesheet, we model formal and actual capacity together — making the gap between contracted and consumed days the central, visible metric.

### Accountable by design
Every entry and change records *who* and *when*. This audit trail replaces the "who edited this cell?" guesswork inherent to shared spreadsheets.

### Finance-ready by default
Covered-day data is structured for the finance template and the monthly (by-the-25th) submission cadence — not reconstructed by hand each cycle.

## Key Features

### Core Capacity Tracking
- **Project profiles:** PMs create a project and define the formally involved experts.
- **Formal load entry:** Contracted days per expert per month (baseline: 20 working days/month).
- **Actual load entry:** Experts record real time spent on tasks.
- **Change attribution:** Every change is stamped with the author and timestamp.

### Views & Visualization
- **Multi-horizon views:** Weekly, monthly, and yearly workload — for both formal and actual levels.
- **Dual presentation:** Every view available in both tabular and graphical form.

### Reporting & Analytics
- **Finance export:** Templated export of covered (paid) days for monthly submission by the 25th.
- **Change analytics:** Analysis of actual-workload changes, broken down per project and per expert, compared against the formal baseline.
