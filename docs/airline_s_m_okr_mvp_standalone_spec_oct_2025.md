# Airline S&M OKR MVP — Standalone Spec
**Date:** Oct 2, 2025  
**Analyst/Author:** Mary (BA)  
**Codename:** "RunwayOKR"

---

## 1) Product vision (updated per constraints)
A **standalone** web app that lets an airline’s **Sales & Marketing** organization turn existing **yearly targets** into clean, quarterly **OKRs**, run lightweight weekly **check‑ins** in‑app (no Slack/Teams), and export a tidy **quarterly review**—all without integrations.

**MVP goal:** Demonstrate OKR value fast: import → transform → track → review.

---

## 2) Scope & non‑goals
**In scope (MVP):** CSV/XLSX import of yearly targets, OKR creation wizard, weekly check‑ins UI, simple dashboards, QBR export, seeded airline S&M templates.  
**Out of scope (MVP):** Slack/Teams/email, Jira/Linear/Asana, SSO/SAML, KPIs beyond simple trendlines, pricing/payments, compliance/audits.

---

## 3) Target users & JTBD (airline S&M)
- **Head of Sales** (Corporate/Trade): wants route/segment revenue targets to become measurable KRs with owners and weekly momentum.  
- **Head of Marketing** (Brand/Performance/CRM): wants campaign and direct‑channel targets mapped into OKRs with clear cadence.  
- **Analysts/CoS:** assemble a quarterly review without chasing updates.

**JTBD:** “Given our yearly targets (revenue, direct share, loyalty enrollments, corporate contracts, campaign ROI), help us define 3–5 objectives with measurable KRs and keep them updated weekly in one place.”

---

## 4) Domain templates (starter library)
- **Direct Channel Growth** — e.g., Direct web share 34% → 40%; App bookings +25%; Abandoned cart 68% → 60%.  
- **Corporate Sales Expansion** — New signed corporate contracts (#); Contracted revenue $X → $Y; RFP win‑rate +pp.  
- **International Premium Revenue** — Premium cabin rev $X → $Y; Upgrade conversions +pp; Partner codeshare revenue +%.  
- **Loyalty & Co‑brand** — Enrollments +%; Co‑brand signups #; Email CTR/CR uplift +pp.  
- **Ancillary Revenue Uplift** — Ancillary per pax $A → $B; Seat/Bag attach rate +pp.

> Units supported at MVP: %, pp (percentage points), $, and #.

---

## 5) Core user flows (MVP)
**Flow A — Import yearly targets → draft OKRs**  
1) Upload CSV/XLSX using provided template.  
2) Map columns (Target Name, Unit, Baseline, Target, Team/Owner, Year).  
3) Wizard groups related targets → proposes Objectives and KRs (editable).  
4) User accepts → creates **Quarter** and assigns KRs to owners.

**Flow B — Weekly check‑ins (in‑app)**  
1) Open **My Week** → list of owned KRs with last value.  
2) Update value, set **Confidence** (Red/Amber/Green), add optional note.  
3) Save → updates trendlines; appears in **Team Dashboard**.

**Flow C — Quarterly review (QBR export)**  
1) Pick Quarter → auto one‑pager: status by Objective, best/worst deltas, stuck KRs (>14d no change).  
2) Export to PDF (basic layout) or copy to clipboard as Markdown.

---

## 6) Information architecture & pages
- **/dashboard** — Company roll‑up, by Objective & Team (RAG, trend).  
- **/okrs** — Grid of Objectives; create/edit; filters by Team & Quarter.  
- **/okrs/new** — 3‑step OKR wizard (from template or from import).  
- **/check‑ins** — “My Week” updates; table + quick inline edit.  
- **/imports** — Upload & mapping; view past imports.  
- **/reviews** — QBR generator; export.  
- **/settings** — Teams, Owners, Units.

---

## 7) Data model (Drizzle/Postgres first pass)
```ts
// db/schema.ts (excerpt)
import { pgTable, serial, varchar, integer, numeric, timestamp, boolean } from "drizzle-orm/pg-core";

export const teams = pgTable('teams', {
  id: serial('id').primaryKey(),
  name: varchar('name', { length: 120 }).notNull(),
});

export const users = pgTable('users', {
  id: serial('id').primaryKey(),
  email: varchar('email', { length: 190 }).notNull(),
  name: varchar('name', { length: 120 }),
  teamId: integer('team_id').references(() => teams.id),
});

export const quarters = pgTable('quarters', {
  id: serial('id').primaryKey(),
  label: varchar('label', { length: 20 }).notNull(), // e.g., 2025‑Q1
  startAt: timestamp('start_at', { withTimezone: true }),
  endAt: timestamp('end_at', { withTimezone: true }),
});

export const objectives = pgTable('objectives', {
  id: serial('id').primaryKey(),
  title: varchar('title', { length: 200 }).notNull(),
  teamId: integer('team_id').references(() => teams.id),
  quarterId: integer('quarter_id').references(() => quarters.id),
  ownerId: integer('owner_id').references(() => users.id),
  confidence: integer('confidence').default(2), // 0=Red,1=Amber,2=Green
});

export const keyResults = pgTable('key_results', {
  id: serial('id').primaryKey(),
  objectiveId: integer('objective_id').references(() => objectives.id).notNull(),
  title: varchar('title', { length: 220 }).notNull(),
  unit: varchar('unit', { length: 8 }).notNull(), // %, pp, $, #
  type: varchar('type', { length: 16 }).notNull(), // percent, absolute, currency, count
  startValue: numeric('start_value'),
  targetValue: numeric('target_value'),
  currentValue: numeric('current_value'),
  direction: varchar('direction', { length: 8 }).default('up'), // up/down
});

export const checkIns = pgTable('check_ins', {
  id: serial('id').primaryKey(),
  krId: integer('kr_id').references(() => keyResults.id).notNull(),
  value: numeric('value').notNull(),
  confidence: integer('confidence').notNull(),
  note: varchar('note', { length: 500 }),
  createdAt: timestamp('created_at', { withTimezone: true }).defaultNow(),
  createdBy: integer('created_by').references(() => users.id),
});

export const imports = pgTable('imports', {
  id: serial('id').primaryKey(),
  filename: varchar('filename', { length: 200 }),
  rows: integer('rows'),
  createdAt: timestamp('created_at', { withTimezone: true }).defaultNow(),
});
```

---

## 8) CSV template (yearly targets)
Columns: **Target Name, Category, Unit (%, pp, $, #), Baseline, Year Target, Team, Owner (email)**  
Example rows:
```
Direct web share, Direct Channel, %, 34, 40, Digital, alice@airline.com
Premium cabin revenue, Premium, $, 120000000, 150000000, Intl Sales, bob@airline.com
Co‑brand card signups, Loyalty, #, 18000, 25000, CRM, chris@airline.com
Ancillary per pax, Ancillary, $, 23.5, 26.0, Revenue Mktg, dana@airline.com
```

---

## 9) OKR creation wizard (copy spec)
- **Step 1: Grouping** — show imported targets by Category; allow regrouping into **Objectives** (drag to group).  
- **Step 2: Drafting** — auto‑compose Objective titles and KR phrasings from each target.  
- **Step 3: Setup** — pick **Quarter**, confirm owners, set starting values; create.

**Rules:** 1–3 Objectives per team; 2–4 KRs per Objective; enforce unit/type consistency; allow “direction = down” for metrics like CPA.

---

## 10) UI components (shadcn/ui)
- **ObjectiveCard** (title, owner, RAG, progress bar, sparkline).  
- **KRRow** (title, unit badge, start → current → target).  
- **CheckInTable** (inline edit, confidence selector, note popover).  
- **ImportMapper** (column dropdowns + preview).  
- **QBRExport** (print‑ready layout with sections: Highlights, Risks, Next Quarter).

---

## 11) Pages & routes (Next.js App Router)
```
/app
  /dashboard/page.tsx
  /okrs/page.tsx
  /okrs/new/page.tsx
  /check-ins/page.tsx
  /imports/page.tsx
  /reviews/page.tsx
  /settings/page.tsx
  /api
    /import/parse/route.ts
    /okrs/create/route.ts
    /check-ins/create/route.ts
```

---

## 12) Airline S&M example OKRs (seed data)
**O1: Grow direct channel share profitably**  
- KR1: Direct web share **34% → 40%** (↑).  
- KR2: App bookings **+25%** vs prior year (↑).  
- KR3: Checkout abandonment **68% → 60%** (↓).

**O2: Expand premium cabin revenue on intl routes**  
- KR1: Premium cabin revenue **$120M → $150M** (↑).  
- KR2: Upgrade conversion rate **+2pp** (↑).  
- KR3: Codeshare partner revenue **+10%** (↑).

**O3: Accelerate loyalty & co‑brand growth**  
- KR1: New program enrollments **+20%** (↑).  
- KR2: Co‑brand card signups **18k → 25k** (↑).  
- KR3: Email campaign conversion **+1.5pp** (↑).

---

## 13) Acceptance criteria (MVP)
- Import wizard accepts the provided CSV, maps columns, and shows a preview.  
- Wizard generates Objectives/KRs exactly from user‑confirmed groupings.  
- Users can perform weekly check‑ins on **/check‑ins** with inline save & undo.  
- **/dashboard** shows Objective RAG, KR progress bars, and a 6‑week sparkline.  
- **/reviews** exports a PDF/print page that fits on 1–2 pages.

---

## 14) Build plan (2 sprints)
**Sprint 1 (App skeleton & import → OKR)**  
- Scaffold routes and Drizzle schema; seed example OKRs.  
- CSV parser + column mapper; wizard step 1–3; create OKRs.

**Sprint 2 (Check‑ins, dashboard, QBR)**  
- Check‑ins table with inline edit + RAG.  
- Dashboard cards + sparklines; QBR export page.  
- Polish & empty‑state content.

---

## 15) Nice‑to‑have (Post‑MVP)
- Simple KPI board view; per‑team views; Markdown editor for review notes.  
- Optional AI assistance for drafting objectives from a pasted annual plan.

