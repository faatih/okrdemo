# Brainstorm — Best UI/UX & Functionality for Airline OKR MVP
**Date:** Oct 2, 2025  
**Agent:** Mary (Business Analyst)  
**Context:** Standalone web app (no integrations) for Airline Sales & Marketing. Built on Next.js Starter Kit foundation. Focus on **working frontend** and **impressive, practical design**.

> This is a living brainstorm to synthesize market patterns into concrete UI/UX and functionality choices for our MVP.

---

## 1) Product north star
- **Demonstrate OKR value fast**: import yearly targets → transform into quarterly OKRs → keep weekly momentum → export a clean review.  
- **Time-to-first‑value < 5 minutes**: frictionless import + opinionated defaults.  
- **Fewer, better goals**: default to **3–5 Objectives** and **2–4 KRs** each; gentle guardrails.

---

## 2) Users & primary outcomes
- **Head of Sales / Marketing**: immediate visibility into 3–5 objectives and whether you’re on track this week.  
- **Managers / Owners**: update KRs quickly (≤60 seconds) without ceremony.  
- **Analysts / CoS**: generate a tidy **QBR one‑pager** without chasing updates.

**Airline S&M outcome themes:** Direct channel growth, Corporate sales, Premium revenue, Loyalty & co‑brand, Ancillary revenue.

---

## 3) MVP surface area (no‑integration version)
**Core flows**  
1) **Import yearly targets** (CSV/XLSX) → map columns → group into Objectives → draft KRs.  
2) **Check‑ins (weekly)**: numeric update + confidence + optional note.  
3) **Dashboard**: objective cards grid with risk rail.  
4) **QBR export**: one‑pager printable view (A4/Letter).  
5) **Settings**: teams, owners, units (% / pp / $ / #).

**Non‑goals (MVP)**: integrations, email/Slack, performance reviews, strategy maps (full), KPI boards (advanced), SSO.

---

## 4) Information architecture & navigation
Top‑level: **Dashboard · OKRs · Check‑ins · Reviews · Imports · Settings**  
- Default landing = **Dashboard** for fast comprehension.  
- **Quarter switcher** in header; Team filter on all key views.  
- **Progressive disclosure**: advanced fields tucked into accordions and drawers.

---

## 5) Screen blueprints
### A) Dashboard (Company roll‑up)
- **Objective Card (grid)**:  
  - Title, owner avatar, **RAG chip + label**, bullet progress bar (start → current → target), **6‑week sparkline**, “last updated” micro‑text.  
  - Click opens **side drawer** with the objective’s KRs (edit inline).  
- **Risk rail (right)**:  
  - **Confidence dropped this week**  
  - **No movement ≥14 days**  
  - **Worst deltas** (top 3).  
- **Design tone**: small multiples; restrained color; whitespace for scannability.

### B) OKRs (manage & edit)
- **Table + drawer** pattern.  
- Guardrails: nudge to **2–4 KRs** per objective, unit picker (%, pp, $, #), allow direction = up/down.  
- Inline “KR quality” hints (clarity, measurability) without scorekeeping.

### C) Check‑ins (My Week)
- **Per‑KR row**: numeric field (prefilled last value), 3‑state confidence (Green/Amber/Red with icons), optional note.  
- **Keyboard‑first**: arrow step, Enter save, undo toast.  
- **Batch save** with diff summary.

### D) Imports (targets → OKRs)
- **Stepper (3)**: Upload → Map columns → Group & draft.  
- Direct‑manipulation grouping (drag cards into Objectives).  
- Preview the results before creating.

### E) Reviews (QBR)
- **One‑pager layout**: objective status, best/worst deltas, stuck KRs, notes.  
- Print styles for A4/Letter.

---

## 6) Airline S&M starter templates (seed content)
- **Direct Channel Growth**: Direct web share 34%→40%; App bookings +25%; Abandonment 68%→60%.  
- **Corporate Sales Expansion**: New corporate contracts #; Contracted revenue $↑; RFP win rate +pp.  
- **International Premium Revenue**: Premium rev $↑; Upgrade conversion +pp; Codeshare rev +%.  
- **Loyalty & Co‑brand**: Enrollments +%; Card signups #; Email conversion +pp.  
- **Ancillary Uplift**: Ancillary per pax $A→$B; Seat/Bag attach rate +pp.

---

## 7) Data‑viz & status patterns
- **Progress vs target**: **Bullet bar** inside cards.  
- **Trend**: **Sparkline** (6 weekly points).  
- **Status**: numeric progress + **confidence (R/A/G)** shown together.  
- Avoid donuts/gauges; favor bars/lines; reduce non‑data ink.

---

## 8) Visual & interaction system
- **Palette**: color‑universal **Okabe–Ito** base; RAG pairs with icons + labels (never hue‑only).  
- **Type scale**: Display 28–32 · Title 20–22 · Body 15–16 · Small 13–14.  
- **Density**: Comfortable default; Compact for tables.  
- **Motion**: 150–200ms subtle fades/slides; skeletons on cards/tables.  
- **Accessibility**: AA contrast, visible focus, keyboard flows everywhere.

---

## 9) Forms & wizard patterns
- **Validation on blur**; errors inline; success toasts with “undo”.  
- **Wizard with progress indicator**; block advance on invalid steps; autosave draft.  
- **Unit‑aware inputs** (%, pp, $, #) with min/max; up/down direction toggle.

---

## 10) Microcopy (voice & tone)
- Objective title prompt: “What outcome, why now?” (one line).  
- KR phrasing pattern: *metric + direction + target + by when*.  
- Confidence prompt: “How likely to hit the target?” (Green/Amber/Red).  
- Empty states: give 1 primary action + sample airline data toggle.

---

## 11) Component inventory (no code, for UI build)
- **ObjectiveCard**, **KRRow**, **ConfidenceChip**, **BulletBar**, **Sparkline**, **RiskRail**, **DrawerForm**, **ImportMapper**, **Stepper**, **EmptyState**, **Toast**, **QuarterSwitcher**, **TeamFilter**.

---

## 12) Functionality backlog (post‑MVP candidates)
- **KPI board** (simple thresholds & trends).  
- **Strategy Map** (collapsed alignment tree).  
- **Inline KR math** (derived KRs from two metrics).  
- **CSV export** for analytics tools.  
- **Localization** (en → tr) & **print language toggle**.

---

## 13) Open decisions
- Confidence scale label set: (On track / At risk / Off track) vs (High / Medium / Low).  
- Offer optional **0.0–1.0 grading** at quarter‑end alongside %?  
- Include light annotations on QBR export (e.g., highlights/risks text blocks)?

---

## 14) Acceptance checklist (frontend only)
- Dashboard grid renders objective cards with **bullet + sparkline**; risk rail filters by **confidence drop** and **staleness ≥14d**.  
- Check‑ins table supports **keyboard‑only** updates with inline validation and optimistic save.  
- Import wizard completes end‑to‑end with **preview** and creates OKRs.  
- Reviews page prints cleanly to **1–2 pages** with the defined typographic scale.

