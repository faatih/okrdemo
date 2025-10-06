# Frontend Architecture

### Component Organization

```
components/
├── ui/                          # shadcn/ui primitives (existing)
├── okr/                         # Domain components (new)
│   ├── objective-card.tsx
│   ├── bullet-bar.tsx
│   ├── sparkline.tsx
│   ├── confidence-chip.tsx
│   ├── kr-row.tsx
│   ├── okr-drawer.tsx
│   ├── risk-rail.tsx
│   └── qbr-layout.tsx
├── wizard/                      # CSV import wizard (new)
│   ├── csv-mapper.tsx
│   ├── target-grouper.tsx
│   ├── okr-drafter.tsx
│   └── okr-finalizer.tsx
└── shared/
    ├── empty-state.tsx
    └── loading-skeleton.tsx
```

### State Management

**State Management Patterns:**
- React Context for simple global state (current quarter, team filters)
- Zustand for complex optimistic UI (check-ins page)
- React Query for server state caching (dashboard data, sparklines)
- Local component state (useState) for UI-only state (modals, accordions)

### Routing

**Route Organization:**
```
app/
├── dashboard/page.tsx          # Story 2.2
├── okrs/
│   ├── page.tsx                # Story 1.8
│   └── new/page.tsx            # Stories 1.5-1.7
├── check-ins/page.tsx          # Story 2.1
├── reviews/page.tsx            # Story 3.1
├── imports/page.tsx            # Story 1.4
└── settings/
    ├── teams/page.tsx          # Story 3.3
    ├── users/page.tsx          # Story 3.4
    ├── quarters/page.tsx       # Story 3.5
    └── units/page.tsx          # Story 3.6
```

---
