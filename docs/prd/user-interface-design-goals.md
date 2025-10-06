# User Interface Design Goals

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
