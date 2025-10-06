# Epic 3: QBR Export & Settings Management

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
