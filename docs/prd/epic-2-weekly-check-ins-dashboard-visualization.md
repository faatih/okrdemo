# Epic 2: Weekly Check-ins & Dashboard Visualization

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
