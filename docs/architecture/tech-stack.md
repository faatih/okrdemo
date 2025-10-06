# Tech Stack

This is the **DEFINITIVE** technology selection for RunwayOKR. All development must use these exact versions. This table represents the final tech stack based on the existing Next.js SaaS Starter Kit 2.0, aligned with PRD requirements.

### Technology Stack Table

| Category | Technology | Version | Purpose | Rationale |
|----------|-----------|---------|---------|-----------|
| **Frontend Language** | TypeScript | 5.x | Type-safe frontend development | PRD requirement, already in starter, prevents runtime errors |
| **Frontend Framework** | Next.js | 15.3.1 | React framework with App Router & SSR | PRD specifies 14+, starter has 15.3.1, provides SSR for fast Dashboard loads |
| **UI Component Library** | shadcn/ui + Radix UI | Latest | Accessible component primitives | PRD specifies shadcn/ui, already in starter, WCAG AA compliant |
| **State Management** | React Context + Zustand | 19.x (React) + 4.x (Zustand) | Client state for check-ins, filters | Lightweight, PRD suggests Context or Zustand, avoid Redux complexity |
| **Backend Language** | TypeScript + Node.js | 5.x (TS) + 18+ (Node) | Type-safe API routes | PRD requirement, serverless functions on Vercel runtime |
| **Backend Framework** | Next.js API Routes | 15.3.1 | Serverless API endpoints | PRD specifies Next.js API routes, collocated with frontend |
| **API Style** | REST | N/A | HTTP JSON endpoints | PRD implies REST (OpenAPI spec mentioned), simple CRUD operations |
| **Database** | Neon PostgreSQL | 15+ | Relational data storage | PRD specifies Neon or Vercel Postgres, starter uses Neon |
| **ORM** | Drizzle ORM | 0.43.1 | Type-safe database queries | PRD requirement, already in starter, generates TS types from schema |
| **Cache** | None (MVP) | N/A | Deferred to Phase 2 | PRD mentions sparkline caching, defer Redis until performance testing |
| **File Storage** | Vercel Blob | Latest | CSV upload temporary storage | PRD specifies Vercel Blob or S3, Vercel Blob simpler for Vercel deployment |
| **Authentication** | Better Auth (Phase 2) | 1.2.8 | Email/password auth | PRD specifies NextAuth, starter has Better Auth, deferred to Phase 2 |
| **Frontend Testing** | Vitest + React Testing Library | Latest | Component unit tests | PRD specifies Vitest + RTL for unit tests |
| **Backend Testing** | Vitest | Latest | API route integration tests | PRD specifies Vitest for integration tests with test DB |
| **E2E Testing** | Playwright (Phase 2) | Latest | End-to-end workflows | PRD defers E2E to Phase 2, manual testing for MVP |
| **Build Tool** | Next.js CLI + Turbopack | 15.3.1 | Development & production builds | Built into Next.js, Turbopack for fast dev builds |
| **Bundler** | Turbopack (dev) + Webpack (prod) | Latest | Module bundling | Next.js default, Turbopack for dev speed, Webpack stable prod |
| **IaC Tool** | None (MVP) | N/A | Manual Vercel config | Infrastructure-as-code deferred, Vercel dashboard sufficient for pilot |
| **CI/CD** | Vercel Git Integration | N/A | Auto-deploy on push | PRD specifies CI/CD, Vercel native integration with GitHub |
| **Monitoring** | Vercel Analytics (basic) | Latest | Performance metrics | PRD defers Sentry/LogRocket to Phase 2, Vercel free tier sufficient |
| **Logging** | Vercel Logs (console.*) | N/A | Server & function logs | PRD: "Basic logging to Vercel logs", no third-party APM for MVP |
| **CSS Framework** | Tailwind CSS | 4.1.7 | Utility-first styling | PRD specifies Tailwind v4, already in starter |
| **Data Visualization** | Recharts | 2.15.3 | Sparklines & bullet bars | PRD recommends Recharts, already in starter, lightweight SVG charts |
| **Form Validation** | Zod + React Hook Form | 3.24.3 (Zod) + 7.56.1 (RHF) | Runtime validation & form handling | PRD specifies Zod for API validation, RHF in starter for forms |
| **CSV Parsing** | PapaParse | 5.x | Client-side CSV parsing | PRD suggests PapaParse, lightweight, browser-based |
| **Email Service (Phase 2)** | Resend or SendGrid | Latest | User invite emails | PRD specifies Resend/SendGrid, deferred to Phase 2 (Story 3.4) |
| **Icons** | Lucide React | 0.503.0 | Icon library | Already in starter, consistent with shadcn/ui |
| **Date Utilities** | date-fns | 4.1.0 | Date formatting & calculations | Already in starter, lightweight alternative to moment.js |
| **Toast Notifications** | Sonner | 2.0.3 | Toast UI feedback | Already in starter, accessible, supports undo pattern |

### Removed from Starter (Not in MVP Scope)

| Technology | Removed | Reason |
|-----------|---------|--------|
| Polar.sh SDK | ❌ | No subscription/payment features in PRD |
| OpenAI SDK | ❌ | No AI chat in PRD scope |
| AWS S3 SDK | ❌ | Using Vercel Blob instead |
| PostHog | ❌ | Analytics deferred to Phase 2 |
| WalletPass | ❌ | Not relevant to OKR tracking |
| UploadThing | ❌ | Using Vercel Blob for CSV uploads |

---
