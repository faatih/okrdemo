# Project Brief: RunwayOKR

**Date:** October 2, 2025
**Version:** 1.0
**Author:** Mary (Business Analyst)

---

## Executive Summary

**RunwayOKR** is a standalone web application that enables airline Sales & Marketing organizations to transform yearly revenue and performance targets into actionable quarterly OKRs with minimal friction. The product solves the critical problem of disconnected goal-setting and tracking by providing a streamlined workflow: import existing targets via CSV, transform them into measurable OKRs through an intelligent wizard, maintain weekly momentum via lightweight check-ins, and generate publication-ready quarterly reviews—all without requiring integrations with Slack, email, or project management tools.

**Target Market:** Mid-to-large airline Sales & Marketing departments (100–500 employees) that already have yearly targets but struggle with quarterly execution visibility and accountability.

**Key Value Proposition:** Demonstrate OKR value in under 5 minutes—from import to first quarterly plan—using airline-specific templates and opinionated defaults that reduce decision fatigue while maintaining flexibility.

---

## Problem Statement

### Current State & Pain Points

Airline Sales & Marketing organizations operate with yearly revenue and performance targets distributed across multiple teams (Direct Channel, Corporate Sales, International Premium, Loyalty, Ancillary Revenue). These targets typically live in spreadsheets, annual planning decks, and email threads. While the *what* is clear (e.g., "Direct web share 34% → 40%"), the quarterly execution cadence is fragmented:

- **No unified tracking system:** Teams chase updates via email, Slack messages, and ad-hoc meetings
- **Inconsistent update rhythm:** Some teams update monthly in slides, others quarterly in spreadsheets, creating visibility gaps
- **Manual quarterly reviews:** Analysts spend 8–12 hours assembling QBR materials by copying data from multiple sources
- **Weak accountability:** Without weekly momentum visibility, at-risk goals stay hidden until quarter-end

### Impact (Quantified)

- **Time waste:** Heads of Sales/Marketing spend ~4 hours/week chasing status updates across 5–8 team leads
- **Late course correction:** Problems surface in Week 10–12 of a 13-week quarter, leaving no time to adjust
- **Review overhead:** Quarterly Business Reviews consume 2–3 days of analyst time for data assembly and formatting
- **Goal dilution:** Without clear priorities, teams track 15–20 metrics instead of focusing on 3–5 critical objectives

### Why Existing Solutions Fall Short

- **Generic OKR tools** (Lattice, Workboard, Ally.io) require integrations, lengthy setup, and don't understand airline S&M domain patterns (direct channel economics, premium cabin revenue, co-brand partnerships)
- **Spreadsheet tracking** works initially but breaks down with 5+ teams due to version control, stale data, and no automated trendlines
- **Project management tools** (Jira, Asana) are built for task execution, not strategic goal tracking with confidence indicators and progress visualization

### Urgency & Importance

Airlines operate in a hyper-competitive, margin-sensitive environment. A 2-point improvement in direct channel share or a 10% lift in ancillary revenue per passenger has multi-million dollar annual impact. The gap between setting ambitious yearly targets and executing them quarterly is where strategic intent dies. Solving this now enables S&M leaders to detect and respond to underperformance within weeks, not months.

---

## Proposed Solution

### Core Concept & Approach

RunwayOKR transforms the chaotic quarterly execution cycle into a predictable four-step workflow:

1. **Import & Transform** – Upload existing yearly targets via CSV/XLSX, map columns automatically, and use an intelligent wizard to group related targets into 3–5 strategic Objectives with 2–4 measurable Key Results each
2. **Weekly Check-ins** – In-app updates (<60 seconds per owner) with numeric progress, confidence indicators (Red/Amber/Green), and optional context notes—no email, no Slack, no ceremony
3. **Live Dashboard** – Real-time company rollup showing Objective status, progress bars, 6-week trend sparklines, and a "risk rail" that surfaces dropped confidence and stalled KRs (no movement ≥14 days)
4. **Quarterly Review Export** – One-click generation of a publication-ready QBR (PDF/Markdown) with highlights, worst deltas, stuck KRs, and formatted for executive consumption

### Key Differentiators from Existing Solutions

- **Domain-Specific Templates:** Pre-built airline S&M patterns (Direct Channel Growth, Corporate Sales Expansion, Premium Revenue, Loyalty & Co-brand, Ancillary Uplift) with appropriate units (%, pp, $, #) and directional logic (up/down)
- **Zero-Integration Architecture:** Standalone web app with no dependencies on Slack/Teams, Jira/Asana, or email—reduces setup friction from days to minutes
- **Opinionated Defaults:** Enforces 3–5 Objectives, 2–4 KRs per Objective, weekly cadence—removes decision paralysis while allowing overrides
- **Fast Time-to-Value:** Import → first quarterly OKR plan in under 5 minutes using existing spreadsheet targets

### Why This Solution Will Succeed Where Others Haven't

1. **Meets users where they are:** Accepts CSV/XLSX targets that already exist rather than forcing a new goal-setting process
2. **No integration tax:** Generic OKR tools fail because airlines won't grant Slack/Jira/SSO access for a pilot—we eliminate that barrier entirely
3. **Domain credibility:** Airline S&M leaders see "Direct web share 34% → 40%" and "Premium cabin revenue $120M → $150M" in templates and immediately recognize their world
4. **Execution focus over planning ceremony:** Weekly check-ins with confidence + sparklines create forward momentum vs. quarterly slide decks that arrive too late

### High-Level Product Vision

A **purpose-built execution layer** for airline Sales & Marketing that sits between annual planning (existing) and daily work (email/meetings), providing the missing quarterly heartbeat with minimal overhead and maximum clarity.

---

## Target Users

### Primary User Segment: Head of Sales / Head of Marketing

**Demographic/Firmographic Profile:**
- **Role:** VP Sales, VP Marketing, Chief Commercial Officer, SVP Revenue Management
- **Organization Size:** Mid-to-large airlines (100–500 employees in S&M organization)
- **Reporting Structure:** Manages 5–8 team leads (Direct Channel, Corporate Sales, International, Loyalty, Ancillary, Brand, Performance Marketing, CRM)
- **Experience Level:** 10–20 years in airline commercial roles; comfortable with BI dashboards (Tableau, Power BI) but frustrated by fragmented data
- **Geography:** Initially US-based carriers; expandable to European/APAC airlines

**Current Behaviors and Workflows:**
- Sets yearly revenue and performance targets in Q4 annual planning cycle (spreadsheet-based with Finance)
- Cascades targets to team leads via email and planning meetings in January
- Reviews progress in monthly leadership meetings (slide deck updates from each team)
- Spends ~4 hours/week in Slack/email asking "where are we on X metric?"
- Assembles quarterly business reviews with analyst support (2–3 days of data gathering)
- Uses spreadsheets for tracking but data goes stale within 2–3 weeks

**Specific Needs and Pain Points:**
- **Fast visibility:** "I need to know if we're on track across 5 teams in under 30 seconds—not by reading 40 slides"
- **Early warning system:** "I want to see confidence dropping or metrics stalling *before* the quarter ends, not after"
- **Minimal overhead:** "My team is already maxed out—any new tool needs to take <1 hour/week total, not add meetings"
- **Executive-ready output:** "I need a clean QBR that I can present to the CEO without reformatting"

**Goals They're Trying to Achieve:**
- Increase accountability across distributed teams without adding bureaucracy
- Shift from reactive (monthly reviews) to proactive (weekly pulse) without increasing meeting load
- Reduce time spent chasing updates from 4 hours/week to <30 minutes/week
- Improve goal achievement rate by surfacing at-risk KRs early enough to course-correct

### Secondary User Segment: KR Owners (Managers & Analysts)

**Demographic/Firmographic Profile:**
- **Role:** Manager of Direct Channel, Corporate Sales Manager, Senior Analyst (Revenue/CRM/Performance Marketing)
- **Team Size:** Manages 3–10 individual contributors or owns specific metrics without direct reports
- **Experience Level:** 5–10 years in airline S&M; comfortable with Excel, light BI tools, CRM dashboards

**Current Behaviors and Workflows:**
- Receives yearly targets from Head of Sales/Marketing via email or planning deck
- Tracks progress in personal spreadsheets or team-specific tools (Google Sheets, Airtable, Salesforce reports)
- Updates leadership via weekly/monthly email summaries or slide updates
- Juggles 8–15 metrics but unclear which 3–5 are "mission critical" for the quarter
- Spends 1–2 hours/week preparing status updates for leadership

**Specific Needs and Pain Points:**
- **Clarity on priorities:** "Which metrics actually matter this quarter vs. nice-to-track?"
- **Quick updates:** "I have the numbers—I just need to log them somewhere without writing an essay"
- **Visibility into peer performance:** "Are other teams on track? Am I the only one struggling?"
- **No double entry:** "I already update my Salesforce dashboard—I don't want to update two systems"

**Goals They're Trying to Achieve:**
- Reduce status update overhead from 1–2 hours/week to <15 minutes/week
- Get clearer direction on what leadership actually cares about (fewer metrics, clearer targets)
- Understand how their KRs contribute to broader team objectives (context, not just numbers)
- Avoid surprise escalations by flagging risks early with confidence indicators

---

## Goals & Success Metrics

### Business Objectives

- **Adoption:** 1 airline S&M organization (100–500 employees) completes full quarterly cycle (import → weekly check-ins → QBR export) within 90 days of launch
- **Time-to-value:** 80% of pilot users complete import → first OKR creation in under 10 minutes (target: 5 minutes)
- **Engagement:** 70% of KR owners complete weekly check-ins ≥10 out of 13 weeks in first quarter
- **Efficiency gain:** Reduce Head of S/M status-chasing time from 4 hours/week to <30 minutes/week (measured via user interview post-quarter)
- **QBR automation:** Generate publication-ready quarterly review in <5 minutes vs. 2–3 days of manual analyst effort

### User Success Metrics

**Primary users (Heads of S/M):**
- Can answer "Are we on track?" in <15 seconds by viewing dashboard
- Export QBR and present to executive leadership without additional formatting
- Identify at-risk KRs via risk rail within first 3 clicks

**Secondary users (KR owners):**
- Complete weekly check-in (value + confidence + note) in <60 seconds
- Understand which KRs they own and current status within first login
- Receive zero Slack/email requests for status updates (all updates flow through app)

**Organizational outcome:**
- At least 1 "at-risk" KR detected and course-corrected mid-quarter (vs. discovered at quarter-end)
- Reduction in number of "status update" meetings from weekly/biweekly to monthly

### Key Performance Indicators (KPIs)

- **Activation rate:** % of invited users who complete first check-in within 7 days of account creation – **Target: 60%**
- **Weekly active users (WAU):** % of KR owners who log in and update ≥1 KR per week – **Target: 70% during quarter**
- **Time-to-first-OKR:** Median time from CSV upload to first Objective created – **Target: <5 minutes**
- **Check-in completion rate:** (# of check-ins completed) / (# of KRs × 13 weeks) – **Target: 65%**
- **Dashboard comprehension:** % of Heads of S/M who can correctly identify top 2 at-risk Objectives in <30 seconds (measured via usability test) – **Target: 90%**
- **QBR export usage:** % of quarters that end with a QBR export generated – **Target: 100%**
- **NPS (Net Promoter Score):** Post-quarter survey – **Target: 40+ (good for B2B SaaS MVP)**

---

## MVP Scope

### Core Features (Must Have)

- **CSV/XLSX Import with Column Mapping:** Upload yearly targets spreadsheet (provided template with columns: Target Name, Category, Unit, Baseline, Year Target, Team, Owner); intelligent column mapper with preview; validation for required fields and unit types (%, pp, $, #)

- **OKR Creation Wizard (3 steps):**
  - Step 1: Group imported targets by Category into proposed Objectives (drag-to-regroup interface)
  - Step 2: Auto-draft Objective titles and KR phrasings from target data (editable)
  - Step 3: Select Quarter, confirm owners, set starting values; enforce 1–3 Objectives per team, 2–4 KRs per Objective

- **Dashboard (Company Roll-up):** Grid of Objective Cards showing title, owner avatar, RAG confidence chip, bullet progress bar (start → current → target), 6-week sparkline, last update timestamp; Quarter selector in header; Team filter; Risk Rail (right sidebar) with "Confidence Dropped," "No Movement ≥14 days," "Worst Deltas"

- **Weekly Check-ins Page ("My Week"):** Table of user's owned KRs with inline editing; numeric input (prefilled with last value), 3-state confidence selector (Red/Amber/Green with icons + labels), optional note field (500 chars); keyboard-first navigation (arrows, Enter to save); batch save with diff summary; undo toast

- **OKRs Management Page:** Table listing all Objectives with filters (Team, Quarter); click row opens side drawer to view/edit KRs inline; add/remove KRs with unit picker; direction toggle (up/down for metrics like CPA or abandonment rate)

- **QBR Export (Quarterly Review):** Auto-generate one-pager with sections: Objective Status Summary, Best/Worst Deltas, Stuck KRs (≥14 days no update), optional notes field; export to print-ready PDF or copy as Markdown; A4/Letter print styles

- **Airline S&M Templates (Seed Data):** 5 pre-built Objective templates with example KRs:
  - Direct Channel Growth (web share %, app bookings %, abandonment rate %)
  - Corporate Sales Expansion (new contracts #, contracted revenue $, RFP win rate pp)
  - International Premium Revenue (premium cabin revenue $, upgrade conversion pp, codeshare revenue %)
  - Loyalty & Co-brand (enrollments %, card signups #, email conversion pp)
  - Ancillary Revenue Uplift (ancillary per pax $, seat/bag attach rate pp)

- **Settings & Admin:** Manage Teams (add/edit/archive); Manage Users (invite via email, assign to teams, set as KR owner); Unit definitions (%, pp, $, #); Quarter setup (label, start/end dates)

- **Empty States & Onboarding:** Dashboard empty state with "Import Targets (CSV)" primary CTA + "Load Sample Airline Data" toggle; OKRs page empty state with example card; Check-ins empty state with scheduled prompt ("First check-in on [next Friday]")

### Out of Scope for MVP

- Slack, Microsoft Teams, or email integrations/notifications
- Jira, Linear, Asana, or project management tool integrations
- SSO/SAML authentication (basic email/password only for MVP)
- Advanced KPI boards with custom thresholds and alerts
- Strategy maps or alignment trees (full visual hierarchy)
- Performance review workflows or 1:1 meeting notes
- Mobile native apps (responsive web only)
- Multi-language localization (English only for MVP)
- Advanced analytics/BI exports or API access
- Role-based permissions beyond owner/editor (single-tier access for MVP)
- Automated reminders or scheduled notifications
- Commenting/discussion threads on KRs
- File attachments or rich text notes

### MVP Success Criteria

- **Import Success:** User can upload provided CSV template, map columns, and create 3–5 Objectives with 10–15 KRs in under 10 minutes
- **Check-in UX:** KR owner completes weekly update (all owned KRs) in under 60 seconds with keyboard-only interaction
- **Dashboard Speed:** Head of S/M can identify company status and top 2 at-risk Objectives in under 15 seconds from landing on dashboard
- **QBR Quality:** Exported quarterly review fits on 1–2 pages and requires zero manual reformatting before presenting to leadership
- **Visual Clarity:** Objective Cards render with bullet graphs + sparklines; Risk Rail correctly filters by confidence drop and staleness; all RAG indicators use color + icons (not color-only)
- **Data Integrity:** Weekly check-ins update currentValue on KRs, trigger sparkline recalculation, and update Objective-level confidence rollup in real-time

---

## Post-MVP Vision

### Phase 2 Features (Next 6 months)

**Integration Layer (Selective):**
- Slack notifications for confidence changes (opt-in, configurable per user)
- CSV export of OKR data for external BI tools (Tableau, Power BI)
- Zapier/Make.com webhooks for custom workflows

**Enhanced KPI Management:**
- Simple KPI board view with threshold indicators (green/amber/red zones based on target %)
- Derived KRs (calculate from two metrics, e.g., "Revenue per Available Seat Mile" = Total Revenue / ASM)
- Historical trend comparison (current quarter vs. prior quarter/year)

**Collaboration & Context:**
- Commenting on KRs with @mentions (limited to app users, no email notifications initially)
- Markdown editor for Objective descriptions and quarterly review notes
- File attachments on Objectives (upload supporting docs like campaign briefs, contract templates)

**Team Views & Permissions:**
- Per-team dashboards (filter by default to "My Team" for non-execs)
- Read-only guest access for C-suite execs (view dashboards, no editing)
- Team-level privacy (hide certain Objectives from cross-team visibility)

**UX Refinements:**
- Inline KR quality scoring (clarity, measurability hints) during creation
- Keyboard shortcuts for power users (J/K navigation, E to edit, C to check-in)
- Dark mode support
- Mobile-optimized views (not native app, but better responsive design for check-ins on-the-go)

### Long-term Vision (12–24 months)

**Become the execution layer for airline commercial organizations** by expanding beyond S&M to Revenue Management, Network Planning, and Customer Experience teams while maintaining the core "import → transform → track → review" simplicity.

**Strategic Alignment Features:**
- Visual strategy map showing Objective → KR → Initiative hierarchy
- Cross-team dependencies (e.g., "Direct Channel Growth" depends on "Digital Platform Reliability" from IT)
- Alignment scoring (what % of company KRs ladder up to top 3 company Objectives)

**AI-Assisted Planning:**
- Natural language import ("Paste your annual plan, we'll suggest OKRs")
- Smart KR suggestions based on historical airline benchmarks (e.g., "Similar airlines improved direct share by 4–6pp in Year 1")
- Automated QBR narrative generation (turn data into executive summary paragraphs)

**Enterprise Readiness:**
- SSO/SAML authentication (Okta, Azure AD)
- Advanced RBAC (role-based access control) with custom permission sets
- Audit logs and compliance reporting
- Multi-tenant architecture with white-label options

**Vertical Expansion:**
- Templates for adjacent airline functions (Revenue Management OKRs, Ops/Customer Experience OKRs)
- Expansion to hospitality (hotel chains with similar S&M structure)
- Generic B2B version (remove airline-specific templates, add customizable domain libraries)

### Expansion Opportunities

**Geographic Expansion:**
- Localization for European airlines (EN, DE, FR, ES)
- APAC airline market (EN, ZH, JA) with cultural adaptation for goal-setting norms
- Middle East carriers (EN, AR) with right-to-left UI support

**Pricing & Monetization:**
- Freemium tier (1 team, 10 KRs, quarterly export only)
- Professional tier ($X/user/month: unlimited teams, integrations, advanced analytics)
- Enterprise tier (SSO, white-label, dedicated support, custom integrations)

**Partner Ecosystem:**
- Pre-built integration templates for airline-specific tools (Sabre, Amadeus, PROS Revenue Management)
- Consulting partnerships with airline strategy firms for OKR transformation services
- Certification program for airline S&M leaders (OKR methodology training + tool mastery)

---

## Technical Considerations

### Platform Requirements

- **Target Platforms:** Web application (desktop-first, responsive for tablet/mobile)
- **Browser Support:**
  - Modern evergreen browsers: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
  - No IE11 support required (airline S&M users typically on modern corporate browsers)
- **Performance Requirements:**
  - Dashboard initial load: <2 seconds on 3G connection
  - Check-in save (single KR): <500ms round-trip
  - CSV import + parsing (100 rows): <5 seconds
  - QBR export generation: <3 seconds
  - Target Lighthouse scores: Performance 90+, Accessibility 95+, Best Practices 90+

### Technology Preferences

- **Frontend:**
  - Next.js 14+ (App Router)
  - React 18+ with TypeScript
  - shadcn/ui component library (accessible, customizable)
  - Tailwind CSS v4 for styling
  - Recharts or lightweight SVG for sparklines/bullet graphs (avoid heavy charting libraries)

- **Backend:**
  - Next.js API routes (serverless functions)
  - Node.js 18+ runtime
  - TypeScript for type safety across full stack

- **Database:**
  - PostgreSQL 15+ (relational model suits OKR hierarchy)
  - Drizzle ORM for type-safe queries
  - Schema: teams, users, quarters, objectives, keyResults, checkIns, imports

- **Hosting/Infrastructure:**
  - Vercel (optimized for Next.js, easy preview deployments, serverless scaling)
  - Vercel Postgres or Neon (managed PostgreSQL with generous free tier)
  - Object storage for CSV uploads: Vercel Blob or AWS S3

### Architecture Considerations

- **Repository Structure:**
  - Monorepo (single Next.js app contains frontend + API routes)
  - `/app` - Next.js App Router pages
  - `/components` - shadcn/ui components + custom components (ObjectiveCard, KRRow, etc.)
  - `/db` - Drizzle schema + migrations
  - `/lib` - Utilities, validation, CSV parsing, QBR generation
  - `/types` - Shared TypeScript types

- **Service Architecture:**
  - Server-side rendering (SSR) for dashboard (SEO not critical, but fast initial paint important)
  - Client-side state management: React Context or Zustand (avoid Redux complexity for MVP)
  - Optimistic UI updates on check-ins (update local state, sync to server, rollback on error)

- **Integration Requirements:**
  - CSV/XLSX parsing: PapaParse or xlsx library
  - PDF generation for QBR: Puppeteer (headless Chrome) or React-PDF (lighter but less flexible)—prefer print CSS + browser print-to-PDF for MVP
  - Email for user invites: Resend or SendGrid (basic transactional only, no marketing emails)

- **Security/Compliance:**
  - Authentication: NextAuth.js with email/password provider (magic links optional)
  - Password hashing: bcrypt or Argon2
  - Row-level security considerations (future): users only see OKRs for their organization (multi-tenant prep)
  - HTTPS only (enforced by Vercel)
  - CSRF protection via NextAuth built-ins
  - Input validation: Zod schemas for all API routes
  - Rate limiting on import/export endpoints (prevent abuse)
  - No PII/sensitive data beyond email + name (no SSN, payment info in MVP)

---

## Constraints & Assumptions

### Constraints

- **Budget:**
  - Development: Self-funded or seed-stage budget (assume solo developer or 2-person team for MVP)
  - Infrastructure: Target <$100/month for MVP pilot (Vercel free tier + Vercel Postgres/Neon free tier should accommodate 100–500 users with moderate usage)
  - Third-party services: <$50/month (email transactional service, monitoring/logging)

- **Timeline:**
  - MVP delivery target: 8–10 weeks (2 sprints per original spec)
  - Sprint 1 (4–5 weeks): App skeleton, Drizzle schema, CSV import + mapper, OKR wizard, seed data
  - Sprint 2 (4–5 weeks): Check-ins UI, dashboard with sparklines, QBR export, empty states, polish
  - Buffer: 2 weeks for testing, bug fixes, pilot onboarding materials

- **Resources:**
  - Team size: 1 full-stack developer (or 1 frontend + 1 backend)
  - Design: Leverage shadcn/ui defaults + Tailwind utilities (minimal custom design work)
  - Domain expertise: Access to 1–2 airline S&M practitioners for validation (interviews, not full-time)
  - Testing: Self-testing + 5–10 alpha users from target airline org

- **Technical:**
  - No existing codebase or legacy system integration (greenfield project)
  - Must use free/freemium tiers of infrastructure for cost constraint
  - CSV import limited to 1000 rows max (airline S&M orgs unlikely to exceed, prevents abuse)
  - QBR export PDF generation via browser print (no server-side PDF rendering to avoid Puppeteer hosting costs)
  - Single-tenant database for MVP (no multi-org isolation, all users in pilot belong to same airline)

### Key Assumptions

**User Assumptions:**
- Target airline S&M org has 100–500 employees but only 20–50 will actively use the tool (Heads of S/M + team leads + select analysts)
- Users have yearly targets already documented in spreadsheets (no net-new goal creation needed for pilot)
- Users comfortable with basic web apps (Google Sheets, Salesforce, Tableau) and don't need extensive hand-holding
- Weekly check-in habit can be established if UX friction is <60 seconds

**Business Assumptions:**
- 1 successful pilot (full quarterly cycle) is sufficient proof-of-concept to raise seed funding or pursue additional pilots
- Airline S&M leaders have discretionary budget ($5–10K/year) to adopt new productivity tools without lengthy procurement
- Word-of-mouth within airline industry networks (conferences, LinkedIn groups) is viable go-to-market for early adopters
- "Standalone, no integrations" is a feature, not a bug, for initial pilots (reduces IT approval complexity)

**Technical Assumptions:**
- PostgreSQL + Drizzle ORM provides sufficient performance for 500 users, 100 Objectives, 400 KRs, 5000 check-ins per quarter
- Vercel's serverless functions handle concurrent check-in updates without race conditions (optimistic locking or last-write-wins acceptable for MVP)
- CSV structure is consistent enough across airlines that column mapper works 80% of time without manual tweaking
- Browser print-to-PDF quality is "good enough" for QBR exports presented to C-suite (no pixel-perfect branding required)

**Market Assumptions:**
- Airline S&M organizations globally share similar pain points (not US-specific)
- OKR methodology is understood or easily explained to airline leaders (not a net-new concept requiring extensive education)
- Competition from generic OKR tools (Lattice, Ally.io) won't aggressively target airline vertical in next 12 months
- Airline industry economic conditions allow S&M teams to focus on execution improvement (not in severe cost-cutting/layoff mode)

---

## Risks & Open Questions

### Key Risks

- **Adoption Risk (User Behavior):** Weekly check-in habit may not stick if users revert to email/Slack updates out of muscle memory. **Impact:** <50% WAU kills value prop; dashboard becomes stale. **Mitigation:** Make check-in UX ridiculously fast (<60s), add weekly calendar reminder template users can self-add, instrument drop-off points to identify friction.

- **CSV Import Quality:** Column mapper may fail if airline target spreadsheets are too inconsistent (merged cells, pivot tables, non-standard units). **Impact:** Users abandon during onboarding; never reach OKR creation. **Mitigation:** Provide strict CSV template with validation rules, offer 15-min onboarding call to guide first import, build robust error messages with example fixes.

- **Organizational Change Resistance:** Heads of S/M may love the tool but team leads resist because "this is just another reporting burden." **Impact:** Leadership can't mandate usage; pilot fails due to incomplete data. **Mitigation:** Position as replacement for existing update mechanisms (not additive), show time savings math (2 hrs/week → 15 min/week), get team lead buy-in during pilot kickoff.

- **Competitive Response:** If MVP gains traction, generic OKR vendors (Lattice, Workboard) could add airline templates and undercut positioning. **Impact:** Loses differentiation; becomes "yet another OKR tool." **Mitigation:** Build deep domain expertise moat (not just templates but airline-specific workflows like seasonal adjustments, route-level KRs), move fast on integrations that matter (Sabre/Amadeus data feeds in Phase 2).

- **Technical Scalability (Phase 2):** Single-tenant MVP architecture requires significant refactor for multi-tenant SaaS. **Impact:** 3–6 month delay between pilot success and commercial launch. **Mitigation:** Design database schema with `organizationId` foreign keys now (unused in MVP but migration-ready), document multi-tenant refactor plan upfront.

- **QBR Export Quality:** Browser print-to-PDF may produce inconsistent results across browsers or fail to meet enterprise branding standards. **Impact:** Users manually reformat exports in PowerPoint; negates "5 minutes vs 2 days" value prop. **Mitigation:** Test print output on Chrome/Firefox/Safari during Sprint 2, offer Markdown export as fallback (users paste into branded template), consider React-PDF if print quality blockers emerge.

### Open Questions

- **Confidence Rollup Logic:** How should Objective-level confidence be calculated from KR confidences? (Average? Worst-case? Weighted by KR importance?) — *Requires user research with pilot team.*

- **Quarter Timing Flexibility:** Do all airlines use calendar quarters (Q1 = Jan–Mar) or do some use fiscal quarters offset from calendar? — *Validate with 2–3 airline contacts before hardcoding quarter dates.*

- **Unit Edge Cases:** How to handle KRs with mixed units (e.g., "Loyalty members: 1.2M → 1.5M" = count in millions vs. raw count)? — *May need unit magnitude selector (K, M, B) in addition to unit type.*

- **Historical Data Import:** Should MVP support importing past quarters for trend comparison, or only current/future quarters? — *Impacts schema design and UX complexity; lean toward "future only" unless pilot explicitly requests.*

- **Team vs. Individual Ownership:** Can a single KR have multiple owners, or strictly one owner per KR? — *Affects check-in UX and accountability model; research best practice from pilot org.*

- **Check-in Edit History:** Should users be able to edit/delete past check-ins, or are they immutable once saved? — *Impacts audit trail and data integrity; consider append-only with "correction" workflow.*

- **Anonymous Feedback on OKRs:** Do users want ability to flag "this KR is unrealistic" without public comments? — *Could surface silent disagreement with targets; requires careful UX to avoid toxicity.*

### Areas Needing Further Research

- **Airline S&M Org Structures:** Variance in team naming conventions (e.g., "Direct Channel" vs. "Digital Commerce" vs. "eCommerce") — conduct 3–5 interviews to build flexible team taxonomy.

- **Existing Tool Landscape:** What BI/tracking tools do target airlines already use? (Tableau, Power BI, Salesforce dashboards, Excel) — understand current workflows to position as complement vs. replacement.

- **Quarterly Review Formats:** What do current QBR decks/documents look like? (Slide count, sections, audience) — get 2–3 examples to ensure export format matches expectations.

- **Seasonal/Cyclical Patterns:** Do airline S&M KRs require seasonal adjustments (e.g., summer travel peaks, holiday booking windows)? — may need "expected trajectory" feature vs. linear progress assumptions.

- **Security/Compliance Requirements:** What data privacy, SOC 2, or audit requirements might airlines impose even on pilot tools? — research typical vendor onboarding checklists to avoid surprises.

- **Pricing Sensitivity:** What's realistic willingness-to-pay per user/month in airline S&M context? — conduct pricing research interviews to inform post-MVP monetization strategy.

---

## Next Steps

### Immediate Actions

1. **Validate airline S&M org structure assumptions** — Conduct 3–5 interviews with airline S&M leaders (target: Heads of Sales/Marketing, team managers) to validate problem statement, team structures, quarterly review processes, and willingness to pilot

2. **Secure pilot partner commitment** — Identify 1 airline S&M organization willing to commit to full quarterly pilot (13 weeks + setup) with 20–50 active users; secure executive sponsor and 2–3 team lead champions

3. **Finalize technical architecture decisions** — Resolve open questions: Vercel Postgres vs. Neon, CSV parsing library, QBR export approach (print CSS vs. React-PDF), confidence rollup formula; document in technical spec

4. **Create project repository and development environment** — Initialize Next.js project with App Router, configure Drizzle ORM, set up Vercel deployment pipeline, establish shadcn/ui component library, create initial DB schema

5. **Design CSV template and example airline data** — Build standardized CSV template with validation rules; create realistic example dataset (50–100 rows) covering all 5 airline S&M templates for onboarding and demos

6. **Build Sprint 1 detailed task breakdown** — Decompose "App skeleton & import → OKR" into atomic tasks with time estimates; identify dependencies and critical path; set up project board (GitHub Projects or Linear)

7. **Establish success metrics instrumentation plan** — Define analytics events to track (time-to-first-OKR, check-in completion rate, dashboard load time); select analytics tool (PostHog, Mixpanel free tier, or custom); implement tracking plan

8. **Research quarterly review format examples** — Collect 2–3 actual QBR documents from airline contacts (anonymized) to inform export layout, typography, sections, and length expectations

---

## PM Handoff

This Project Brief provides the full context for **RunwayOKR**. Please start in **'PRD Generation Mode'**, review the brief thoroughly to work with the user to create the PRD section by section as the template indicates, asking for any necessary clarification or suggesting improvements.

**Key Context for PRD Development:**

- **Core Value Proposition:** Import existing yearly targets → transform to quarterly OKRs → maintain weekly momentum → export clean QBR (all in <5 minutes time-to-value)
- **Critical Success Factor:** Weekly check-in adoption (70% WAU target) — UX must be <60 seconds per user
- **Domain Specificity:** 5 airline S&M templates are table stakes for credibility, not nice-to-have
- **Architecture Constraint:** Single-tenant MVP, but design schema for future multi-tenant migration
- **Open Research Needs:** Confidence rollup logic, quarter timing (calendar vs. fiscal), seasonal adjustment patterns

**PRD Should Emphasize:**

1. Detailed user flows with edge cases (import failure states, concurrent check-in conflicts, empty states)
2. Component specifications (ObjectiveCard, KRRow, BulletBar, Sparkline) with data bindings and interaction states
3. API endpoint contracts (request/response schemas, validation rules, error codes)
4. Database schema refinements (indexes, constraints, foreign keys, migration strategy)
5. Acceptance criteria per feature (testable, measurable, tied to success metrics)

---

*Generated by Mary (Business Analyst) on October 2, 2025*
