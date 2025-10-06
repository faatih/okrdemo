# Epic 1: Foundation & CSV Import to OKR Transformation

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
