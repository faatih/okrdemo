# OKR MVP — Frontend Design Research & Decisions
**Date:** Oct 2, 2025  
**Focus:** Working frontend and impressive design decisions (no integrations)  
**Audience:** Design + Frontend for Airline Sales & Marketing MVP

> This document synthesizes best‑practice research for OKR software UX and maps it to concrete UI decisions for our standalone MVP. (Citations are in chat.)

---

## 1) Experience goals (what “good” looks like)
- **Fast comprehension:** Exec can grasp status of 3–5 objectives in <15s.  
- **Zero‑friction updates:** KR check‑ins in <60s per owner.  
- **Good defaults:** 3–5 KRs per objective; weekly update rhythm; simple RAG + trend.  
- **Clarity over chrome:** Prefer simple visuals (bars/lines/bullets) over gauges/donuts.  
- **Accessible by default:** Colorblind‑safe palette + WCAG‑AA contrast.

---

## 2) Information architecture & navigation
- **Top‑level:** Dashboard · OKRs · Check‑ins · Reviews · Imports · Settings.  
- **Default landing:** Dashboard (company rollup) with switcher for Quarter.  
- **Progressive disclosure:** Advanced fields hidden behind “Advanced” accordions; minimal fields shown by default.

---

## 3) Primary screens (MVP)
### A) Dashboard (roll‑up)
- **Header strip:** Quarter selector, team filter, “Add Objective” primary action.  
- **Objective Cards (grid):** title, owner avatar, RAG chip, bullet graph (start→current→target), 6‑week sparkline, last update timestamp.  
- **Risk rail (right):** “Confidence ↓” list + “No movement 14d+”.  
- **Design notes:** small multiples; avoid donuts/gauges; keep color sparing (labels + icons).

### B) OKRs (manage)
- **Table + drawer:** table lists Objectives; selecting opens side‑drawer to edit KRs.  
- **Inline add:** 2–4 KRs per Objective enforced by UI hints; unit picker (%, pp, $, #).  
- **Alignment (post‑MVP):** show subtle “Strategy Map” preview as a collapsed tree (prep for V1).

### C) Check‑ins (My Week)
- **List per KR:** numeric input with last value prefilled, confidence selector (Red/Amber/Green), optional note.  
- **Keyboard first:** up/down arrows to step values; Enter to save; undo toast.  
- **Batch submit:** “Save all” with diff summary.

### D) Imports (targets → OKRs)
- **Stepper (3 steps):** Upload → Map columns → Group into Objectives & draft KRs.  
- **Direct manipulation:** drag targets into Objective groups; enforce 2–4 KRs per Objective with gentle guardrails.  
- **Review:** show result preview before creating records.

### E) Reviews (QBR export)
- **One‑pager layout:** Objective status, best/worst deltas, stuck KRs, notes.  
- **Export:** print‑ready PDF styling (A4/Letter).

---

## 4) Visual language
- **Color palette (color‑blind friendly):** use Okabe–Ito set (blue, orange, green, red, purple, amber, gray, black).  
- **RAG chips:** avoid pure red/green dependence; pair with icons + labels; use teal/orange/red variants with high contrast.  
- **Typography:** Display (28–32), Title (20–22), Body (15–16), Small (13–14).  
- **Density modes:** Comfortable (default) & Compact (tables).  
- **Layout:** 12‑column grid; 16–24px spacing scale; 8px baseline for compact areas.

---

## 5) Data‑viz patterns (for OKRs)
- **KR progress vs target:** **Bullet graph** (start|current|target band) inside Objective Card.  
- **Trend over time:** **Sparkline** (6 points: weekly).  
- **Overview charts:** use bars/lines only; avoid pie/donut/gauge.  
- **Status semantics:** numeric % complete + confidence (R/A/G) shown together.

---

## 6) Check‑in interaction model
- **Update cadence:** weekly.  
- **Controls:** numeric stepper; confidence as 3‑state segmented control with tooltips.  
- **Microcopy:** “How likely to hit target?” for confidence; “What changed?” for note.  
- **Autosave + optimistic UI** with inline validation for numeric ranges and units.

---

## 7) Forms & validation
- **Inline validation** after field blur; errors next to fields; positive confirmation on success.  
- **Multi‑step wizard** uses progress indicator + “Back” persistence; prevent advance on invalid steps.  
- **Numeric rules:** unit‑aware inputs (%, pp, $, #) with min/max and directional hints.

---

## 8) Empty states & onboarding
- **Dashboard empty:** illustration + “Import targets (CSV)” primary + “Start with templates” secondary; sample airline S&M data toggle.  
- **OKRs empty:** show example Objective card with ghost content; CTA “Create your first OKR”.  
- **Check‑ins empty:** scheduled note (“First weekly check‑in on Friday”).

---

## 9) Accessibility notes (AA baseline)
- **Contrast:** aim 4.5:1 for text; 3:1 for large text & UI components.  
- **Non‑color cues:** icons/labels with RAG; tooltips never color‑only.  
- **Focus:** visible focus rings; keyboard access for all inputs; target size ≥ 24px.

---

## 10) Motion & micro‑interactions
- **Subtle only:** fade/slide 150–200ms; E‑out.  
- **Skeletons:** on Objective Cards and table rows.  
- **Toasts:** confirm saves; include undo.

---

## 11) Components (shadcn/ui)
- **ObjectiveCard**, **KRRow**, **ConfidenceChip**, **Sparkline**, **BulletBar**, **ImportMapper**, **Stepper**, **DrawerForm**, **EmptyState**, **Toast**.

---

## 12) Frontend build notes (no code)
- Use Starter Kit’s Tailwind v4, shadcn/ui, dark mode, skeletons, optimistic updates.  
- Keep charts as lightweight SVG components (no heavy libs initially).  
- Set up CSS variables for palette + elevation; use data‑density attribute for modes.

---

## 13) Content guidelines
- **Objective title:** action‑oriented, one line.  
- **KR phrasing:** metric + direction + target + timeframe (e.g., “Direct web share 34% → 40% by Q2”).  
- **Confidence labels:** Green = On track; Amber = At risk; Red = Off track.

---

## 14) MVP acceptance (frontend)
- Dashboard loads with Objective Cards + bullet + sparkline; risk rail filters correctly.  
- Check‑ins page supports keyboard‑only updates; inline validation; optimistic save.  
- Import wizard creates OKRs and shows preview state; empty states designed for all key pages.  
- Reviews page prints to 1–2 pages with clean typographic scale.

