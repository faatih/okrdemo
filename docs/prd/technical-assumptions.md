# Technical Assumptions

### Repository Structure: Monorepo

Single Next.js repository containing frontend (React components, pages) and backend (API routes, serverless functions). Directory structure:
- `/app` - Next.js App Router pages and layouts
- `/components` - shadcn/ui components + custom components (ObjectiveCard, KRRow, BulletBar, Sparkline, etc.)
- `/db` - Drizzle schema definitions and migrations
- `/lib` - Utilities, validation helpers, CSV parsing, QBR generation logic
- `/types` - Shared TypeScript types and interfaces
- `/public` - Static assets

### Service Architecture

**Monolith with serverless API routes.** Next.js 14+ App Router with server-side rendering (SSR) for Dashboard (fast initial paint). API routes deployed as serverless functions on Vercel. Client-side state management using React Context or Zustand (avoid Redux complexity). Optimistic UI updates for check-ins. PostgreSQL 15+ relational database via Drizzle ORM. Authentication via NextAuth.js (email/password provider). CSV/XLSX parsing client-side using PapaParse or xlsx library. PDF generation via browser print-to-PDF (print CSS, no Puppeteer to reduce hosting costs).

**Database schema (Drizzle/PostgreSQL):**
- `teams` (id, name)
- `users` (id, email, name, teamId)
- `quarters` (id, label, startAt, endAt)
- `objectives` (id, title, teamId, quarterId, ownerId, confidence)
- `keyResults` (id, objectiveId, title, unit, type, startValue, targetValue, currentValue, direction)
- `checkIns` (id, krId, value, confidence, note, createdAt, createdBy)
- `imports` (id, filename, rows, createdAt)

**Critical:** Schema includes unused `organizationId` foreign keys on major tables (teams, users, quarters, objectives) to support future multi-tenant migration without major refactor.

### Testing Requirements

**Unit + Integration testing for MVP.**
- **Unit tests:** Critical business logic (OKR creation wizard, confidence rollup calculations, CSV parsing/validation, QBR generation)
- **Integration tests:** API routes (create OKR, save check-in, export QBR) with test database
- **Manual testing:** UI workflows (import CSV, weekly check-ins, dashboard filters, QBR export) via 5-10 alpha users from pilot airline
- **No E2E automation for MVP** (Playwright/Cypress deferred to Phase 2) - rely on manual testing and real pilot usage
- **Testing tools:** Vitest for unit/integration, React Testing Library for component tests
- **CI/CD:** Run tests on Vercel preview deployments, block merges on test failures

### Additional Technical Assumptions and Requests

- **Hosting:** Vercel (optimized for Next.js, free tier sufficient for pilot, easy preview deployments, serverless scaling)
- **Database:** Vercel Postgres or Neon (managed PostgreSQL, generous free tier, <100ms latency from Vercel functions)
- **Object Storage:** Vercel Blob or AWS S3 for CSV uploads (temporary storage, 7-day retention)
- **Email Service:** Resend or SendGrid (transactional only, <$50/month, no marketing emails)
- **Frontend Tech Stack:**
  - Next.js 14+ (App Router)
  - React 18+ with TypeScript
  - shadcn/ui component library (accessible, customizable, Radix UI primitives)
  - Tailwind CSS v4 for styling
  - Recharts or lightweight SVG for sparklines/bullet graphs (avoid Chart.js/D3.js bundle bloat)
- **Backend Tech Stack:**
  - Next.js API routes (serverless functions)
  - Node.js 18+ runtime
  - TypeScript for type safety across full stack
  - Drizzle ORM for type-safe queries
- **Data Visualization:** Prefer simple SVG components for Objective Card sparklines (6 data points, weekly) and bullet bars (start→current→target) over heavy charting libraries
- **Input Validation:** Zod schemas for all API routes (runtime + compile-time type safety, auto-generates TypeScript types)
- **Concurrency:** Last-write-wins acceptable for MVP on concurrent check-in updates (optimistic locking deferred to Phase 2)
- **Observability:** Basic logging to Vercel logs (console.log/error), no third-party APM for MVP (defer Sentry/LogRocket to Phase 2)
- **Feature Flags:** Not required for MVP (single-tenant pilot, direct deployments)

---
