# RunwayOKR Product Requirements Document (PRD)

**Project:** RunwayOKR
**Version:** 1.0
**Date:** October 2, 2025
**Author:** John (Product Manager)
**Status:** Draft

---

## Goals and Background Context

### Goals

- Enable airline S&M organizations to transform yearly targets into quarterly OKRs in under 5 minutes (import → first OKR created)
- Achieve 70% weekly active user rate among KR owners during the quarter (10+ weeks out of 13)
- Reduce Head of S/M status-chasing time from 4 hours/week to <30 minutes/week
- Enable weekly check-in completion in <60 seconds per KR owner
- Generate publication-ready quarterly business reviews in <5 minutes (vs. 2-3 days manual effort)
- Deliver MVP within 8-10 weeks using standalone architecture (no Slack/Teams/Jira integrations)
- Demonstrate measurable OKR value through 1 complete pilot (100-500 employee airline S&M org)

### Background Context

Airline Sales & Marketing organizations struggle with the execution gap between yearly revenue targets and quarterly results. While targets exist in spreadsheets (Direct Channel, Corporate Sales, Premium Revenue, Loyalty, Ancillary), teams lack a unified system for weekly momentum tracking. Heads of S/M spend ~4 hours/week chasing updates via email/Slack, problems surface too late (Week 10-12 of 13-week quarters), and quarterly reviews consume 2-3 days of analyst time assembling data from fragmented sources.

Generic OKR tools (Lattice, Workboard, Ally.io) require lengthy setup and integrations that create IT approval barriers for pilots. RunwayOKR solves this with a standalone web app that accepts existing CSV targets, transforms them via an intelligent wizard into 3-5 Objectives with 2-4 KRs each, maintains weekly check-ins with confidence indicators (Red/Amber/Green), and exports clean QBRs—all without dependencies on external tools. The product targets mid-to-large airlines (100-500 S&M employees) with domain-specific templates (direct channel economics, premium cabin revenue, co-brand partnerships) that provide immediate credibility and fast time-to-value.

### Change Log

| Date | Version | Description | Author |
|------|---------|-------------|--------|
| 2025-10-02 | 1.0 | Initial PRD draft based on Project Brief | John (PM) |

---

## Requirements

### Functional Requirements

**FR1:** The system shall accept CSV/XLSX file uploads containing yearly targets with columns: Target Name, Category, Unit (%, pp, $, #), Baseline, Year Target, Team, Owner (email)

**FR2:** The system shall provide an intelligent column mapper that previews uploaded data and allows users to map source columns to required fields with validation

**FR3:** The system shall support a 3-step OKR creation wizard: (1) Group targets by Category into Objectives with drag-to-regroup UI, (2) Auto-draft Objective titles and KR phrasings (editable), (3) Select Quarter, confirm owners, set starting values

**FR4:** The system shall enforce guardrails of 1-3 Objectives per team and 2-4 KRs per Objective with gentle UI hints

**FR5:** The system shall support 4 unit types: % (percent), pp (percentage points), $ (currency), # (count) with appropriate formatting and validation

**FR6:** The system shall allow KRs to have directional targets (up or down) to support metrics like abandonment rate or cost-per-acquisition where lower is better

**FR7:** The system shall provide a Dashboard page showing a grid of Objective Cards with: title, owner avatar, RAG confidence chip, bullet progress bar (start→current→target), 6-week sparkline, last update timestamp

**FR8:** The system shall include a Risk Rail (sidebar) on the Dashboard filtering Objectives by: "Confidence Dropped," "No Movement ≥14 days," "Worst Deltas"

**FR9:** The system shall provide Quarter selector in header and Team filter on Dashboard

**FR10:** The system shall provide a "My Week" check-ins page listing all KRs owned by the current user with inline editing

**FR11:** The system shall support weekly check-in workflow: numeric input (prefilled with last value), 3-state confidence selector (Red/Amber/Green with icons + labels), optional note field (500 chars max)

**FR12:** The system shall support keyboard-first navigation on check-ins page (arrow keys, Enter to save, batch save with diff summary, undo toast)

**FR13:** The system shall provide an OKRs management page with table listing all Objectives, filterable by Team and Quarter

**FR14:** The system shall open a side drawer when Objective row is clicked, allowing inline view/edit of associated KRs

**FR15:** The system shall provide a QBR export feature that auto-generates a one-pager with sections: Objective Status Summary, Best/Worst Deltas, Stuck KRs (≥14 days no update), optional notes field

**FR16:** The system shall support QBR export to print-ready PDF (via browser print) and copy-as-Markdown

**FR17:** The system shall include 5 pre-built airline S&M templates with example OKRs: Direct Channel Growth, Corporate Sales Expansion, International Premium Revenue, Loyalty & Co-brand, Ancillary Revenue Uplift

**FR18:** The system shall provide Settings & Admin pages to manage Teams (add/edit/archive), Users (invite via email, assign to teams, set as KR owner), Unit definitions, Quarter setup (label, start/end dates)

**FR19:** The system shall provide empty states for Dashboard, OKRs, and Check-ins pages with primary CTAs ("Import Targets (CSV)", "Load Sample Airline Data" toggle, "Create your first OKR")

**FR20:** The system shall update KR currentValue in real-time when check-ins are saved, trigger sparkline recalculation, and update Objective-level confidence rollup

**FR21:** The system shall support user authentication via email/password (NextAuth.js)

**FR22:** The system shall send transactional emails for user invites using Resend or SendGrid

**FR23:** The system shall store all check-in history with timestamps and created-by user references

**FR24:** The system shall limit CSV import to 1000 rows maximum to prevent abuse

**FR25:** The system shall validate all numeric inputs for KRs based on unit type and direction (e.g., percentages 0-100, currency > 0)

### Non-Functional Requirements

**NFR1:** Dashboard initial load time shall be <2 seconds on 3G connection

**NFR2:** Check-in save (single KR) shall complete round-trip in <500ms

**NFR3:** CSV import + parsing (100 rows) shall complete in <5 seconds

**NFR4:** QBR export generation shall complete in <3 seconds

**NFR5:** The application shall achieve Lighthouse scores: Performance 90+, Accessibility 95+, Best Practices 90+

**NFR6:** The application shall support modern evergreen browsers: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+ (no IE11 support)

**NFR7:** The application shall use HTTPS only (enforced by hosting platform)

**NFR8:** The application shall implement CSRF protection via NextAuth built-ins

**NFR9:** The application shall hash passwords using bcrypt or Argon2

**NFR10:** The application shall validate all API route inputs using Zod schemas

**NFR11:** The application shall implement rate limiting on import/export endpoints

**NFR12:** The application shall use optimistic UI updates on check-ins (update local state, sync to server, rollback on error)

**NFR13:** The application shall remain within <$100/month infrastructure costs for MVP pilot (100-500 users)

**NFR14:** All RAG indicators shall use color + icons (not color-only) for colorblind accessibility

**NFR15:** The application shall maintain WCAG AA contrast ratios: 4.5:1 for text, 3:1 for large text & UI components

**NFR16:** The application shall provide visible focus rings and keyboard access for all inputs with target size ≥24px

**NFR17:** The application shall implement single-tenant database architecture with schema designed for future multi-tenant migration (include organizationId foreign keys, unused in MVP)

**NFR18:** The application shall store no PII/sensitive data beyond email and name (no SSN, payment info)

---

## User Interface Design Goals

### Overall UX Vision

RunwayOKR prioritizes **speed and clarity** over feature richness. The user experience centers on three core moments: (1) **Fast comprehension** - executives grasp status of 3-5 objectives in <15 seconds via Dashboard, (2) **Zero-friction updates** - KR owners complete check-ins in <60 seconds with keyboard-only workflow, (3) **Good defaults** - opinionated guardrails (3-5 KRs per objective, weekly rhythm, simple RAG + trend) reduce decision fatigue while maintaining flexibility. Visual language emphasizes **small multiples** (Objective Cards in grid), **restrained color** (colorblind-safe palette with icons), and **clarity over chrome** (bars/lines/bullets instead of gauges/donuts).

### Key Interaction Paradigms

- **Progressive disclosure:** Advanced fields hidden behind accordions; minimal fields shown by default
- **Direct manipulation:** Drag-to-regroup targets into Objectives during wizard; inline editing throughout
- **Keyboard-first:** Arrow keys for navigation, Enter to save, undo toasts, batch operations
- **Optimistic UI:** Immediate visual feedback on check-ins with server sync and rollback on error
- **Table + drawer pattern:** List views open side drawers for detail/edit (avoids full page navigation)
- **Microcopy guidance:** Prompts like "How likely to hit target?" for confidence, "What changed?" for notes

### Core Screens and Views

1. **Dashboard (Company Roll-up)** - Default landing page showing grid of Objective Cards with Risk Rail sidebar
2. **OKRs Management** - Table of all Objectives with Team/Quarter filters and side drawer for KR editing
3. **Check-ins ("My Week")** - List of owned KRs with inline editing for weekly updates
4. **OKR Creation Wizard (3 steps)** - Import → Map → Group/Draft workflow
5. **Imports** - CSV upload interface with column mapper and preview
6. **Reviews (QBR Export)** - One-pager layout with print styles and Markdown export
7. **Settings** - Teams, Users, Units, Quarter configuration
8. **Login/Auth** - Email/password authentication (NextAuth.js)

### Accessibility: WCAG AA

- Contrast ratios: 4.5:1 for text, 3:1 for large text & UI components
- Non-color cues: Icons + labels with RAG chips, tooltips never color-only
- Focus visibility: Clear focus rings, keyboard access for all inputs, target size ≥24px
- Colorblind-safe palette: Use Okabe-Ito color set (blue, orange, green, red, purple, amber, gray, black)

### Branding

**Minimal custom branding for MVP.** Leverage shadcn/ui defaults with Tailwind v4 utilities. Color palette restricted to colorblind-friendly Okabe-Ito set. Typography scale: Display (28-32px), Title (20-22px), Body (15-16px), Small (13-14px). Density modes: Comfortable (default) and Compact (tables). Layout: 12-column grid, 16-24px spacing scale, 8px baseline for compact areas. Subtle motion: 150-200ms fades/slides with ease-out. Skeletons for loading states. Toasts for confirmations with undo.

### Target Device and Platforms: Web Responsive

Desktop-first responsive web application (no native mobile apps for MVP). Optimized for modern corporate browsers on desktop/laptop screens (1366x768 minimum). Responsive design supports tablet landscape (1024x768) and mobile portrait (375x667) for check-ins on-the-go, but primary usage expected on desktop. Progressive enhancement approach: core functionality works on all screen sizes, advanced features (drag-to-regroup, complex sparklines) may degrade gracefully on smaller screens.

---

## Technical Assumptions

### Repository Structure: Monorepo

Single Next.js repository containing frontend (React components, pages) and backend (API routes, serverless functions). Directory structure:
- `/app` - Next.js App Router pages and layouts
- `/components` - shadcn/ui components + custom components (ObjectiveCard, KRRow, BulletBar, Sparkline, etc.)
- `/db` - Drizzle schema definitions and migrations
- `/lib` - Utilities, validation helpers, CSV parsing, QBR generation logic
- `/types` - Shared TypeScript types and interfaces
- `/public` - Static assets

### Service Architecture

**Monolith with serverless API routes.** Next.js 14+ App Router with server-side rendering (SSR) for Dashboard (fast initial paint). API routes deployed as serverless functions on Vercel. Client-side state management using React Context or Zustand (avoid Redux complexity). Optimistic UI updates for check-ins. PostgreSQL 15+ relational database via Drizzle ORM. Authentication via NextAuth.js (email/password provider). CSV/XLSX parsing client-side using PapaParse or xlsx library. PDF generation via browser print-to-PDF (print CSS, no Puppeteer to reduce hosting costs).

**Database schema (Drizzle/PostgreSQL):**
- `teams` (id, name)
- `users` (id, email, name, teamId)
- `quarters` (id, label, startAt, endAt)
- `objectives` (id, title, teamId, quarterId, ownerId, confidence)
- `keyResults` (id, objectiveId, title, unit, type, startValue, targetValue, currentValue, direction)
- `checkIns` (id, krId, value, confidence, note, createdAt, createdBy)
- `imports` (id, filename, rows, createdAt)

**Critical:** Schema includes unused `organizationId` foreign keys on major tables (teams, users, quarters, objectives) to support future multi-tenant migration without major refactor.

### Testing Requirements

**Unit + Integration testing for MVP.**
- **Unit tests:** Critical business logic (OKR creation wizard, confidence rollup calculations, CSV parsing/validation, QBR generation)
- **Integration tests:** API routes (create OKR, save check-in, export QBR) with test database
- **Manual testing:** UI workflows (import CSV, weekly check-ins, dashboard filters, QBR export) via 5-10 alpha users from pilot airline
- **No E2E automation for MVP** (Playwright/Cypress deferred to Phase 2) - rely on manual testing and real pilot usage
- **Testing tools:** Vitest for unit/integration, React Testing Library for component tests
- **CI/CD:** Run tests on Vercel preview deployments, block merges on test failures

### Additional Technical Assumptions and Requests

- **Hosting:** Vercel (optimized for Next.js, free tier sufficient for pilot, easy preview deployments, serverless scaling)
- **Database:** Vercel Postgres or Neon (managed PostgreSQL, generous free tier, <100ms latency from Vercel functions)
- **Object Storage:** Vercel Blob or AWS S3 for CSV uploads (temporary storage, 7-day retention)
- **Email Service:** Resend or SendGrid (transactional only, <$50/month, no marketing emails)
- **Frontend Tech Stack:**
  - Next.js 14+ (App Router)
  - React 18+ with TypeScript
  - shadcn/ui component library (accessible, customizable, Radix UI primitives)
  - Tailwind CSS v4 for styling
  - Recharts or lightweight SVG for sparklines/bullet graphs (avoid Chart.js/D3.js bundle bloat)
- **Backend Tech Stack:**
  - Next.js API routes (serverless functions)
  - Node.js 18+ runtime
  - TypeScript for type safety across full stack
  - Drizzle ORM for type-safe queries
- **Data Visualization:** Prefer simple SVG components for Objective Card sparklines (6 data points, weekly) and bullet bars (start→current→target) over heavy charting libraries
- **Input Validation:** Zod schemas for all API routes (runtime + compile-time type safety, auto-generates TypeScript types)
- **Concurrency:** Last-write-wins acceptable for MVP on concurrent check-in updates (optimistic locking deferred to Phase 2)
- **Observability:** Basic logging to Vercel logs (console.log/error), no third-party APM for MVP (defer Sentry/LogRocket to Phase 2)
- **Feature Flags:** Not required for MVP (single-tenant pilot, direct deployments)

---

## Epic List

**Epic 1: Foundation & CSV Import to OKR Transformation**
Goal: Establish project infrastructure, authentication, and core CSV import workflow that transforms yearly targets into quarterly OKRs

**Epic 2: Weekly Check-ins & Dashboard Visualization**
Goal: Enable KR owners to perform weekly check-ins and provide executives with real-time dashboard showing Objective status, trends, and risk indicators

**Epic 3: QBR Export & Settings Management**
Goal: Allow users to generate publication-ready quarterly reviews and manage teams, users, quarters, and units via Settings

---

## Epic 1: Foundation & CSV Import to OKR Transformation

**Epic Goal:** Establish the foundational Next.js application with authentication, database schema, and the complete CSV import-to-OKR workflow. Users should be able to upload a CSV of yearly targets, map columns, group them into Objectives, and create a quarter's worth of OKRs—all within 5 minutes. This epic delivers the first major value: transforming fragmented spreadsheet targets into structured, trackable OKRs.

### Story 1.1: Project Setup & Health Check

**As a** developer,
**I want** a fully configured Next.js project with TypeScript, Tailwind v4, shadcn/ui, Drizzle ORM, and Vercel deployment,
**so that** the team has a solid foundation to build features and a health check endpoint to verify deployments.

#### Acceptance Criteria

1. Next.js 14+ App Router project initialized with TypeScript, ESLint, Prettier
2. Tailwind CSS v4 configured with shadcn/ui component library installed
3. Drizzle ORM configured with PostgreSQL connection (Vercel Postgres or Neon)
4. Git repository created with `.gitignore`, initial commit, and `main` branch
5. Vercel project linked with CI/CD pipeline (auto-deploy on push to `main`, preview on PRs)
6. Health check API route (`/api/health`) returns `{ status: "ok", timestamp: <ISO> }` with 200 status
7. Root page (`/`) displays "RunwayOKR" heading and link to health check (temporary landing page)
8. README.md includes setup instructions, environment variable template, and architecture overview
9. Project successfully deploys to Vercel and health check endpoint is accessible

### Story 1.2: Database Schema & Migrations

**As a** developer,
**I want** complete Drizzle schema definitions for teams, users, quarters, objectives, keyResults, checkIns, and imports,
**so that** the application has a fully typed, relational database foundation to support OKR workflows.

#### Acceptance Criteria

1. `db/schema.ts` defines all tables per PRD Technical Assumptions: teams, users, quarters, objectives, keyResults, checkIns, imports
2. Schema includes unused `organizationId` columns on teams, users, quarters, objectives (for future multi-tenant migration)
3. Foreign key relationships defined: users→teams, objectives→quarters/teams/users, keyResults→objectives, checkIns→keyResults/users
4. Unit types enumerated: %, pp, $, # (string column with validation)
5. Direction types enumerated: up, down (string column)
6. Confidence types enumerated: 0=Red, 1=Amber, 2=Green (integer column)
7. Drizzle migrations generated and applied to development database
8. Seed script creates 2 teams, 5 users, 1 quarter (2025-Q1), and sample airline S&M data (3 Objectives, 10 KRs) per FR17
9. Database connection verified via simple query in health check endpoint

### Story 1.3: Authentication (Email/Password)

**As a** user,
**I want** to log in with my email and password,
**so that** I can access my organization's OKRs securely.

#### Acceptance Criteria

1. NextAuth.js configured with email/password provider (credentials)
2. Login page (`/login`) with email and password inputs, "Sign In" button, basic validation
3. Password hashing implemented using bcrypt or Argon2 (NFR9)
4. Session management via NextAuth with secure HTTP-only cookies
5. Protected routes redirect to `/login` if user not authenticated (middleware check)
6. Logout functionality accessible via user menu in header
7. User creation endpoint (`POST /api/auth/signup`) for initial user registration (manual, no self-service signup for MVP)
8. Login successful redirects to `/dashboard` (placeholder page)
9. CSRF protection enabled via NextAuth built-ins (NFR8)

### Story 1.4: CSV Import - Upload & Column Mapping

**As a** Head of Sales/Marketing,
**I want** to upload my yearly targets CSV and map the columns to required fields,
**so that** I can import my existing data without manual reformatting.

#### Acceptance Criteria

1. Import page (`/imports`) with file upload component (accepts .csv and .xlsx, max 1000 rows per FR24)
2. CSV template provided as downloadable file (`/templates/targets-template.csv`) with required columns: Target Name, Category, Unit, Baseline, Year Target, Team, Owner
3. Client-side CSV parsing using PapaParse or xlsx library (parse on upload, display preview)
4. Column mapper UI shows source columns (from uploaded file) and target fields (required schema) with dropdown selectors
5. Preview table displays first 10 rows with mapped columns highlighted
6. Validation errors shown inline: missing required fields, invalid unit types (must be %, pp, $, #), invalid email format for Owner, numeric validation for Baseline/Year Target
7. "Continue to Wizard" button disabled until all required columns mapped and validation passes
8. Import record created in `imports` table with filename, row count, timestamp on successful parse
9. Parsed data stored in session/temporary storage for next wizard step (not persisted to DB yet)

### Story 1.5: OKR Creation Wizard - Step 1 (Group Targets)

**As a** Head of Sales/Marketing,
**I want** to group related yearly targets into strategic Objectives,
**so that** I can organize my KRs by theme (Direct Channel, Corporate Sales, etc.).

#### Acceptance Criteria

1. Wizard Step 1 page (`/okrs/new?step=1`) displays parsed targets as draggable cards grouped by Category column
2. Each category group has editable title (defaults to Category value from CSV)
3. User can drag target cards between groups to regroup
4. User can create new group with custom title (e.g., split "Corporate Sales" into "Domestic" and "International")
5. UI enforces 1-3 Objectives per team guideline with gentle warning (not hard block) per FR4
6. "Back" button returns to column mapper, "Next" proceeds to Step 2
7. Grouped data persisted in session/temporary storage
8. Progress indicator shows Step 1 of 3

### Story 1.6: OKR Creation Wizard - Step 2 (Draft Objectives & KRs)

**As a** Head of Sales/Marketing,
**I want** the system to auto-draft Objective titles and KR phrasings from my grouped targets,
**so that** I can quickly review and refine them instead of writing from scratch.

#### Acceptance Criteria

1. Wizard Step 2 page (`/okrs/new?step=2`) displays each group from Step 1 as an Objective with auto-drafted title
2. Objective title auto-generation logic: "Grow [Category]" or "Expand [Category]" based on target direction
3. Each target within group becomes a KR with phrasing: "[Target Name] [Baseline] → [Year Target] [Unit]"
4. User can edit Objective titles and KR phrasings inline
5. User can remove KRs or reorder them within an Objective
6. UI enforces 2-4 KRs per Objective guideline with gentle warning (not hard block) per FR4
7. Direction (up/down) inferred from unit type (default: up, but user can toggle per FR6)
8. "Back" button returns to Step 1, "Next" proceeds to Step 3
9. Draft OKRs persisted in session/temporary storage
10. Progress indicator shows Step 2 of 3

### Story 1.7: OKR Creation Wizard - Step 3 (Finalize & Create)

**As a** Head of Sales/Marketing,
**I want** to select the quarter, confirm owners, and set starting values for my OKRs,
**so that** I can create a complete quarterly plan ready for tracking.

#### Acceptance Criteria

1. Wizard Step 3 page (`/okrs/new?step=3`) displays all drafted Objectives and KRs from Step 2
2. Quarter selector dropdown populated from `quarters` table (create Q1 2025 if not exists)
3. For each Objective: confirm owner (dropdown of users from same team, default to CSV Owner if exists)
4. For each KR: confirm owner (dropdown, default to CSV Owner), set starting value (default to Baseline from CSV)
5. User can override starting values, target values, and owners
6. "Back" button returns to Step 2, "Create OKRs" button submits
7. API route (`POST /api/okrs/create`) validates and inserts Objectives and KRs into database (transaction)
8. Success: redirect to `/okrs` with toast "X Objectives and Y Key Results created successfully"
9. Failure: display validation errors inline, do not create partial data
10. Progress indicator shows Step 3 of 3
11. Import record updated with reference to created OKRs

### Story 1.8: OKRs Management Page

**As a** Head of Sales/Marketing,
**I want** to view all Objectives in a table and edit their KRs in a side drawer,
**so that** I can manage my quarterly goals without navigating multiple pages.

#### Acceptance Criteria

1. OKRs page (`/okrs`) displays table of all Objectives with columns: Title, Owner (avatar + name), Team, Quarter, Confidence (RAG chip), # of KRs
2. Filters: Team dropdown (all teams + "All Teams"), Quarter dropdown (all quarters + current quarter default)
3. Click on Objective row opens side drawer (right side, overlay)
4. Drawer displays Objective title (editable), owner, and list of associated KRs
5. Each KR row shows: title, unit badge, start value, current value, target value, direction (up/down icon), owner
6. User can inline edit KR title, values, direction within drawer
7. "Add KR" button in drawer creates new KR with unit picker (%, pp, $, #) per FR5
8. "Delete KR" icon on KR row (confirmation modal)
9. "Save" button in drawer updates Objective and KRs (API: `PATCH /api/okrs/:id`)
10. Close drawer returns to table view
11. Empty state: "No OKRs yet. Import targets to get started." with CTA to `/imports`

### Story 1.9: Empty States & Sample Data Toggle

**As a** new user,
**I want** to see helpful empty states and load sample airline data,
**so that** I can understand the product without importing my own CSV first.

#### Acceptance Criteria

1. Dashboard empty state (`/dashboard`): illustration + "Import Targets (CSV)" primary button + "Load Sample Airline Data" toggle per FR19
2. OKRs page empty state: example Objective card (ghost content) + "Create your first OKR" CTA
3. Check-ins page empty state: "First check-in on [next Friday]" scheduled note (calculate next Friday from today)
4. "Load Sample Airline Data" toggle triggers API call (`POST /api/seed/sample`) that creates 2 teams, 5 users, 1 quarter, 5 Objectives (per airline S&M templates from FR17), 15 KRs with initial check-ins
5. Sample data creation shows loading spinner, then redirects to `/dashboard` with toast "Sample data loaded successfully"
6. Sample data toggle only visible when database is empty (no Objectives exist)
7. All empty states follow shadcn/ui EmptyState component pattern with consistent styling

---

## Epic 2: Weekly Check-ins & Dashboard Visualization

**Epic Goal:** Enable KR owners to perform weekly updates in under 60 seconds and provide executives with a real-time Dashboard showing Objective status, 6-week trends, and proactive risk indicators. This epic delivers the second major value: maintaining weekly momentum and fast executive visibility without chasing updates via email/Slack.

### Story 2.1: Check-ins Page ("My Week")

**As a** KR owner,
**I want** to update my owned KRs quickly with new values and confidence levels,
**so that** I can complete my weekly check-in in under 60 seconds.

#### Acceptance Criteria

1. Check-ins page (`/check-ins`) displays table of all KRs owned by current user (filter: `keyResults.ownerId = currentUser.id`)
2. Table columns: KR Title, Objective (parent title), Last Value, New Value (input), Confidence (3-state selector), Note (optional, 500 chars max per FR11)
3. New Value input prefilled with last check-in value (or startValue if no check-ins yet)
4. Confidence selector: 3-state segmented control with icons + labels (Red="Off track", Amber="At risk", Green="On track") per FR11
5. Keyboard-first navigation: Tab between inputs, Enter to save current row, Shift+Enter for batch save per FR12
6. "Save All" button at bottom with diff summary modal ("You're updating X KRs. Review changes?")
7. API route (`POST /api/check-ins`) creates check-in records, updates KR currentValue, recalculates sparkline data
8. Optimistic UI: immediate visual update on save, undo toast if save fails per NFR12
9. Success toast: "Check-ins saved successfully" with undo link (reverts to previous values if clicked within 10s)
10. Check-in save completes in <500ms round-trip per NFR2
11. Empty state: "No KRs assigned to you yet" if user owns no KRs

### Story 2.2: Dashboard - Objective Cards Grid

**As a** Head of Sales/Marketing,
**I want** to see all Objectives at a glance with status, progress, and trends,
**so that** I can understand if we're on track in under 15 seconds.

#### Acceptance Criteria

1. Dashboard page (`/dashboard`) displays grid of Objective Cards (3-4 columns responsive) per FR7
2. Each Objective Card shows: title, owner avatar + name, RAG confidence chip (color + icon + label), bullet progress bar (start→current→target aggregated from KRs), 6-week sparkline, "Last updated X days ago" timestamp
3. Bullet progress bar visualization: gray background (full range start→target), colored fill (start→current), target marker (vertical line)
4. Sparkline: 6 data points (weekly aggregated currentValue from check-ins), simple SVG line chart
5. Click on Objective Card opens same side drawer as OKRs page (view/edit KRs)
6. Confidence chip uses colorblind-safe Okabe-Ito palette with icons (not color-only) per NFR14
7. Quarter selector in header (dropdown, defaults to current quarter) per FR9
8. Team filter in header (dropdown: "All Teams" + individual teams) per FR9
9. Dashboard loads in <2 seconds on 3G connection per NFR1
10. Empty state: "No Objectives for this quarter. Import targets or create OKRs." with CTA

### Story 2.3: Dashboard - Risk Rail

**As a** Head of Sales/Marketing,
**I want** to see which Objectives are at risk (confidence dropped, no movement, worst deltas),
**so that** I can proactively address problems before quarter-end.

#### Acceptance Criteria

1. Risk Rail displays in right sidebar on Dashboard (collapsible, default open) per FR8
2. Section 1: "Confidence Dropped" - lists Objectives where confidence changed from Green→Amber or Amber→Red in past 7 days
3. Section 2: "No Movement ≥14 days" - lists Objectives where no KR check-ins recorded in past 14 days (stale)
4. Section 3: "Worst Deltas" - lists top 3 Objectives with largest negative delta between current and expected progress (expected = linear interpolation from start to target based on weeks elapsed)
5. Each risk item shows: Objective title, brief reason ("Confidence dropped to Red", "No updates for 18 days", "15% behind target"), click to focus Objective Card
6. Risk Rail updates in real-time when check-ins saved or filters changed
7. Empty state per section: "No at-risk Objectives" with checkmark icon
8. Risk Rail responsive: collapses to drawer on mobile/tablet, accessible via icon button

### Story 2.4: Sparkline Data Calculation

**As a** system,
**I want** to calculate 6-week sparkline data from check-in history,
**so that** Objective Cards can display trend visualizations accurately.

#### Acceptance Criteria

1. API endpoint (`GET /api/objectives/:id/sparkline`) returns 6 data points (weekly aggregated)
2. Aggregation logic: for each of past 6 weeks (Sun-Sat), average all KR currentValues from check-ins within that week
3. If no check-ins in a week, use previous week's value (flat line) or startValue for first week
4. Sparkline data cached for 1 hour (Redis or in-memory cache) to reduce DB queries
5. Sparkline recalculated when new check-in saved (invalidate cache)
6. Data returned as JSON: `{ weeks: ["2025-W01", "2025-W02", ...], values: [34.5, 36.2, ...] }`
7. Frontend renders sparkline using lightweight SVG component (Recharts or custom SVG)
8. Sparkline shows trend only (no axes, labels, or grid) for minimal visual footprint

### Story 2.5: Confidence Rollup Logic

**As a** system,
**I want** to calculate Objective-level confidence from KR confidences,
**so that** Objective Cards display accurate RAG status.

#### Acceptance Criteria

1. Confidence rollup logic: Objective confidence = worst KR confidence (conservative approach: if any KR is Red, Objective is Red)
2. Alternative logic (configurable setting for future): average KR confidences, round down (Green=2, Amber=1, Red=0 → avg ≥1.5 = Green, ≥0.5 = Amber, <0.5 = Red)
3. Rollup calculated on-the-fly when Objective queried (no stored confidence column, derive from KRs)
4. API endpoint (`GET /api/objectives/:id`) includes `confidence` field in response
5. Rollup logic unit tested with edge cases: all Green KRs, mixed confidences, no check-ins yet (default to Amber)
6. Rollup updates immediately when check-in saved (optimistic UI on frontend, confirmed on next fetch)

---

## Epic 3: QBR Export & Settings Management

**Epic Goal:** Enable users to generate publication-ready quarterly business reviews in under 5 minutes and manage foundational data (teams, users, quarters, units) via Settings. This epic completes the MVP by delivering the final major value: automated QBR generation (vs. 2-3 days manual effort) and self-service administration for pilot teams.

### Story 3.1: QBR Export - One-Pager Layout

**As a** Head of Sales/Marketing,
**I want** to generate a clean one-pager quarterly review,
**so that** I can present results to the CEO without manual reformatting.

#### Acceptance Criteria

1. Reviews page (`/reviews`) with Quarter selector and "Generate QBR" button per FR15
2. API endpoint (`GET /api/reviews/:quarterId`) generates one-pager with sections: Objective Status Summary (table: Objective, Owner, Confidence, Progress %), Best Deltas (top 3 KRs with highest positive delta), Worst Deltas (top 3 KRs with highest negative delta), Stuck KRs (list KRs with no check-ins ≥14 days), Notes (optional textarea for user-added commentary)
3. One-pager layout uses print-friendly CSS: A4/Letter page size, clean typography (Title 20-22px, Body 15-16px per branding guidelines), margins for printing
4. QBR generation completes in <3 seconds per NFR4
5. Preview rendered in browser before export (user can review before printing/copying)
6. Notes field autosaved to `quarters` table (metadata column)

### Story 3.2: QBR Export - PDF & Markdown

**As a** Head of Sales/Marketing,
**I want** to export the QBR as PDF or Markdown,
**so that** I can share it in different formats.

#### Acceptance Criteria

1. "Print to PDF" button triggers browser print dialog with print CSS optimized for QBR layout per FR16
2. "Copy as Markdown" button copies QBR content to clipboard in Markdown format (tables, headings, bullet lists)
3. Markdown format includes: `## Objective Status Summary`, table with pipes, `### Best Deltas`, bullet list, etc.
4. Print CSS ensures 1-2 page max (fit on A4/Letter), no page breaks mid-section
5. PDF export tested on Chrome, Firefox, Safari (ensure consistent output per Risk: QBR Export Quality from Brief)
6. Success toast after copy: "QBR copied to clipboard" with undo (if browser supports)
7. Fallback: if browser print not supported, show message "Please use Chrome, Firefox, or Safari for PDF export"

### Story 3.3: Settings - Teams Management

**As a** admin user,
**I want** to create, edit, and archive teams,
**so that** I can organize users and OKRs by department.

#### Acceptance Criteria

1. Settings page (`/settings/teams`) displays table of all teams: Name, # of Users, # of Objectives, Actions (Edit, Archive) per FR18
2. "Add Team" button opens modal with Name input, "Create" button
3. Edit team: modal with Name input (pre-filled), "Save" button updates `teams` table
4. Archive team: confirmation modal ("This will hide the team but not delete data"), sets `archived` flag (soft delete)
5. Archived teams hidden from dropdowns/filters but data retained
6. Validation: team name required, max 120 chars
7. API routes: `POST /api/teams`, `PATCH /api/teams/:id`, `DELETE /api/teams/:id` (soft delete)

### Story 3.4: Settings - Users Management

**As a** admin user,
**I want** to invite users, assign them to teams, and set them as KR owners,
**so that** I can onboard my pilot team.

#### Acceptance Criteria

1. Settings page (`/settings/users`) displays table of all users: Name, Email, Team, # of Owned KRs, Actions (Edit, Deactivate) per FR18
2. "Invite User" button opens modal with Email, Name, Team dropdown, "Send Invite" button
3. Invite triggers transactional email via Resend/SendGrid with temporary password (or magic link for passwordless, deferred to Phase 2)
4. Edit user: modal with Name, Team, "Save" button updates `users` table
5. Deactivate user: confirmation modal, sets `active` flag to false (soft delete), user cannot log in
6. Validation: email required and valid format, name required, max 120 chars
7. API routes: `POST /api/users/invite`, `PATCH /api/users/:id`, `DELETE /api/users/:id` (soft delete)
8. Email template: "You've been invited to RunwayOKR. Your temporary password is: [generated]. Please log in and change your password."

### Story 3.5: Settings - Quarters Setup

**As a** admin user,
**I want** to create and configure quarters,
**so that** I can set up quarterly planning cycles.

#### Acceptance Criteria

1. Settings page (`/settings/quarters`) displays table of all quarters: Label (e.g., "2025-Q1"), Start Date, End Date, # of Objectives, Actions (Edit, Archive) per FR18
2. "Add Quarter" button opens modal with Label input, Start Date picker, End Date picker, "Create" button
3. Edit quarter: modal with fields pre-filled, "Save" button updates `quarters` table
4. Archive quarter: confirmation modal, sets `archived` flag (soft delete)
5. Validation: label required (format: YYYY-QX or custom), start/end dates required, end > start, no overlapping quarters
6. Default quarter suggestions: if no quarters exist, suggest current and next quarter with auto-calculated dates (Q1=Jan-Mar, Q2=Apr-Jun, Q3=Jul-Sep, Q4=Oct-Dec)
7. API routes: `POST /api/quarters`, `PATCH /api/quarters/:id`, `DELETE /api/quarters/:id` (soft delete)
8. Open question from Brief: validate calendar vs. fiscal quarter assumption with pilot (note in UI: "Quarters default to calendar quarters. Contact us for fiscal quarter support.")

### Story 3.6: Settings - Units Configuration

**As a** admin user,
**I want** to view and confirm supported unit types,
**so that** I understand what metrics I can track.

#### Acceptance Criteria

1. Settings page (`/settings/units`) displays table of supported units: Symbol (%, pp, $, #), Name (Percent, Percentage Points, Currency, Count), Format Example (34%, +2pp, $120M, 18,000) per FR5
2. Read-only for MVP (no custom units in MVP, deferred to Phase 2)
3. Help text: "These are the supported unit types for Key Results. Custom units and magnitude selectors (K, M, B) are planned for future releases."
4. Note open question from Brief: "For metrics in millions/billions (e.g., $120M), enter raw values ($120000000) and we'll format them in reports. Enhanced formatting coming soon."

### Story 3.7: Header Navigation & User Menu

**As a** user,
**I want** consistent navigation and access to settings/logout,
**so that** I can easily move between pages and manage my account.

#### Acceptance Criteria

1. Header component with logo ("RunwayOKR"), navigation links (Dashboard, OKRs, Check-ins, Reviews, Imports, Settings), user menu (avatar + name dropdown)
2. User menu dropdown: Profile (future), Settings (link to `/settings/teams`), Logout
3. Active page highlighted in navigation (underline or background color)
4. Header responsive: collapses to hamburger menu on mobile/tablet
5. Header present on all authenticated pages, hidden on `/login`
6. Logo links to `/dashboard` (home)

### Story 3.8: Performance Optimization & Final Polish

**As a** user,
**I want** the application to load quickly and feel responsive,
**so that** I can complete my workflows efficiently.

#### Acceptance Criteria

1. Dashboard initial load <2 seconds on 3G per NFR1 (verified via Lighthouse throttling)
2. Check-in save <500ms round-trip per NFR2 (verified via browser DevTools Network tab)
3. CSV import + parsing (100 rows) <5 seconds per NFR3 (verified with test CSV)
4. QBR export generation <3 seconds per NFR4 (verified with test data)
5. Lighthouse scores achieved: Performance 90+, Accessibility 95+, Best Practices 90+ per NFR5
6. Image optimization: use Next.js Image component, WebP format where supported
7. Code splitting: dynamic imports for heavy components (wizard steps, drawer, modals)
8. Database query optimization: add indexes on foreign keys (teamId, quarterId, ownerId, krId), analyze slow queries with `EXPLAIN`
9. Caching: sparkline data cached for 1 hour, quarter/team/user lists cached for 5 minutes
10. Error boundaries: catch React errors, display friendly "Something went wrong" message with reload button
11. Loading states: skeletons for Objective Cards, table rows during fetch
12. Toast notifications: consistent positioning (bottom-right), auto-dismiss after 5s, accessible (screen reader announcements)

---

## Checklist Results Report

### PM Checklist Results

**Checklist Execution Date:** October 2, 2025

#### 1. Goals Clarity
✅ **PASS** - Goals section clearly defines 7 measurable outcomes (5-minute time-to-value, 70% WAU, status-chasing time reduction, <60s check-ins, QBR automation, 8-10 week delivery, 1 pilot completion)

#### 2. Requirements Completeness
✅ **PASS** - 25 Functional Requirements and 18 Non-Functional Requirements cover all features from Project Brief MVP scope. Requirements traceable to Brief sections (CSV import, wizard, dashboard, check-ins, QBR, settings, templates, empty states).

#### 3. UI/UX Specification
✅ **PASS** - UI Design Goals section comprehensively covers UX vision (speed + clarity), interaction paradigms (progressive disclosure, keyboard-first, optimistic UI), 8 core screens, WCAG AA accessibility with specific contrast ratios and colorblind considerations, branding guidelines (typography, spacing, motion), and responsive web platform strategy.

#### 4. Technical Assumptions Documented
✅ **PASS** - Technical Assumptions section specifies monorepo structure, Next.js/React/TypeScript stack, Drizzle/PostgreSQL schema, Vercel hosting, testing approach (unit + integration, manual for UI), and critical architectural decisions (serverless, optimistic UI, print-to-PDF for QBR, single-tenant with multi-tenant prep).

#### 5. Epic Sequencing
✅ **PASS** - 3 epics follow logical progression: (1) Foundation + CSV→OKR (core value: transformation), (2) Check-ins + Dashboard (core value: momentum + visibility), (3) QBR + Settings (core value: automation + admin). Each epic delivers deployable, testable functionality.

#### 6. Story Sizing
✅ **PASS** - 19 stories across 3 epics. Each story scoped for 2-4 hour AI agent execution ("junior developer" heuristic). Vertical slices: Story 1.4 (CSV upload + mapping), Story 2.1 (check-ins page), Story 3.1 (QBR layout). Enablers integrated into value-delivering stories (e.g., Story 1.2 database schema includes seed data).

#### 7. Acceptance Criteria Quality
✅ **PASS** - All stories have 6-12 acceptance criteria defining "done" from functional perspective. Criteria are testable (e.g., "Dashboard loads in <2 seconds on 3G per NFR1", "Check-in save completes in <500ms per NFR2"), unambiguous (specific API routes, UI elements, validation rules), and include NFRs where critical (performance, accessibility, security).

#### 8. Dependency Mapping
✅ **PASS** - Story dependencies implicitly clear via epic sequencing. Epic 1 establishes foundation (auth, schema, import→OKR) before Epic 2 (check-ins require KRs from Epic 1, dashboard requires check-in data). Epic 3 builds on Epics 1-2 (QBR requires check-in history, settings manages entities created in Epic 1). No story depends on work from later epic.

#### 9. Cross-Cutting Concerns
✅ **PASS** - Authentication (Story 1.3) delivered in Epic 1 before feature stories. Performance optimization (Story 3.8) at end but includes verification of NFRs established throughout (dashboard load, check-in save, CSV parsing, QBR generation). Logging, error handling, loading states integrated into individual stories' acceptance criteria (e.g., optimistic UI in Story 2.1, error boundaries in Story 3.8).

#### 10. Alignment with Brief
✅ **PASS** - PRD directly maps to Project Brief:
- Goals section extracts Brief's Business Objectives + User Success Metrics
- Requirements section implements Brief's MVP Scope (Core Features + Out of Scope enforcement)
- UI Design Goals section incorporates Brief's UX goals (fast comprehension, zero-friction updates, good defaults, visual language)
- Technical Assumptions section uses Brief's Technical Considerations verbatim (Next.js, Drizzle, Vercel, etc.)
- Epic structure delivers Brief's 4-step workflow (import→transform→check-in→review)
- All 5 airline S&M templates from Brief included in Story 1.2 seed data and FR17
- Open questions from Brief noted in Settings stories (calendar vs. fiscal quarters, confidence rollup logic, unit edge cases)

**Overall Assessment:** ✅ **PRD READY FOR ARCHITECTURE PHASE**

All checklist items pass. PRD provides sufficient detail for UX Expert and Architect to proceed. No blocking gaps identified.

**Recommendations for Next Phase:**
1. UX Expert should create wireframes for wizard steps (drag-to-regroup UI in Story 1.5 needs visual specification)
2. Architect should confirm Vercel Postgres vs. Neon decision and document migration strategy for multi-tenant (per NFR17)
3. Architect should design sparkline/bullet bar SVG components or select Recharts configuration (per Story 2.2, 2.4)
4. PM to validate with pilot airline: calendar vs. fiscal quarters, confidence rollup formula preference (worst-case vs. average), unit magnitude needs (K/M/B)

---

## Next Steps

### UX Expert Prompt

Please review the **RunwayOKR PRD** (docs/prd.md) and the **Project Brief** (docs/brief.md). Create detailed wireframes and interaction specifications for the following priority flows:

1. **CSV Import & OKR Creation Wizard (3 steps)** - Focus on drag-to-regroup UI in Step 1, auto-drafted content editing in Step 2, and Quarter/Owner selection in Step 3
2. **Dashboard with Objective Cards Grid + Risk Rail** - Specify Objective Card component layout (bullet bar, sparkline, RAG chip positioning), Risk Rail sections, and responsive behavior
3. **Check-ins Page ("My Week")** - Detail inline editing UX, keyboard navigation, batch save flow, and undo toast behavior
4. **QBR Export Layout** - Design print-ready one-pager with sections (Objective Status, Best/Worst Deltas, Stuck KRs, Notes)

Reference the **UI Design Goals** section for constraints: WCAG AA accessibility, colorblind-safe palette (Okabe-Ito), typography scale, keyboard-first interactions, optimistic UI patterns. Deliverable: Figma wireframes or annotated sketches with component specs ready for Architect to implement.

### Architect Prompt

Please review the **RunwayOKR PRD** (docs/prd.md), the **Project Brief** (docs/brief.md), and the forthcoming UX wireframes. Design the technical architecture for MVP delivery in 8-10 weeks. Prioritize:

1. **Database Schema Refinement** - Confirm Drizzle schema from Story 1.2, add indexes for performance (NFR1-4), document multi-tenant migration path (organizationId columns per NFR17)
2. **API Route Contracts** - Define request/response schemas for all endpoints (use Zod), error codes, validation rules (reference FR1-25, NFR10)
3. **Component Architecture** - Specify ObjectiveCard, KRRow, BulletBar, Sparkline, ConfidenceChip implementations (shadcn/ui + custom SVG per Technical Assumptions)
4. **State Management Strategy** - Document React Context or Zustand patterns for check-ins page, dashboard filters, wizard multi-step state
5. **Performance Strategy** - Address NFR1-4 with caching plan (sparkline data, lookups), query optimization (EXPLAIN plans), code splitting (wizard, drawer)
6. **Testing Approach** - Set up Vitest for unit/integration, document test cases for critical business logic (OKR creation, confidence rollup, CSV parsing, QBR generation)

Reference the **Technical Assumptions** section for tech stack decisions. Deliverable: Architecture document (docs/architecture.md) with diagrams, API specs, component hierarchy, and implementation guidance for stories. Flag any open questions or risks requiring PM clarification before Epic 1 begins.

---

*Generated by John (Product Manager) on October 2, 2025*
