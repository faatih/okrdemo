# Requirements

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
