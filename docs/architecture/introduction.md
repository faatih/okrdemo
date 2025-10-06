# Introduction

This document outlines the complete fullstack architecture for **RunwayOKR**, a specialized OKR tracking platform for airline Sales & Marketing organizations. The architecture covers backend systems, frontend implementation, and their integration, serving as the single source of truth for AI-driven development.

**Project Context:**
- **Base Template**: Next.js SaaS Starter Kit 2.0 (simplified for MVP)
- **Development Timeline**: 8-10 weeks to MVP
- **Target**: Single-tenant pilot (100-500 users at mid-to-large airline)
- **Core Value**: Transform yearly targets into quarterly OKRs in <5 minutes, maintain weekly momentum with <60s check-ins, generate QBRs in <5 minutes

This unified architecture combines traditional backend and frontend concerns into a cohesive document optimized for rapid AI-driven fullstack development within tight timeline constraints.

### Starter Template: Next.js SaaS Starter Kit 2.0

**Based On:** Next.js SaaS Starter Kit 2.0 (existing codebase)

**Starter Features Analysis:**

| Feature | Status | Rationale |
|---------|--------|-----------|
| **Next.js 15 + App Router** | ✅ **KEEP** | Aligns with PRD (Next.js 14+), provides latest features |
| **TypeScript** | ✅ **KEEP** | PRD requirement for type safety |
| **Tailwind CSS v4** | ✅ **KEEP** | Exact match with PRD specs |
| **shadcn/ui + Radix UI** | ✅ **KEEP** | PRD specifies shadcn/ui for accessible components |
| **Neon PostgreSQL** | ✅ **KEEP** | PRD Technical Assumptions specify Neon as option |
| **Drizzle ORM** | ✅ **KEEP** | PRD specifies Drizzle for type-safe queries |
| **Better Auth v1.2.8** | ✅ **KEEP** | Supports email/password auth (PRD FR21) |
| **Polar.sh Payments** | ❌ **REMOVE** | Not in MVP scope, no subscription model |
| **OpenAI Chat** | ❌ **REMOVE** | Not in PRD scope |
| **Cloudflare R2 Storage** | ❌ **REMOVE** | PRD uses Vercel Blob/S3 for CSV uploads only |
| **PostHog Analytics** | ❌ **REMOVE** | Deferred to Phase 2 per PRD |
| **Google OAuth** | 🔄 **DEFER** | PRD specifies email/password for MVP, OAuth future |
| **Dark/Light Theme** | ✅ **KEEP** | Good UX practice, minimal overhead |
| **Recharts** | ✅ **KEEP** | PRD recommends Recharts for sparklines/bullet graphs |

**Architectural Constraints from Starter:**
- Existing directory structure: `/app`, `/components`, `/db`, `/lib`, `/hooks`
- Better Auth session management already configured
- Database connection pattern established with Drizzle
- API route patterns in place
- Component library (shadcn/ui) already installed

**Simplification Strategy:**
1. **Remove unused routes**: `/dashboard/chat`, `/dashboard/upload`, `/dashboard/payment`, `/pricing`
2. **Remove dependencies**: `@polar-sh/sdk`, `@ai-sdk/openai`, `@aws-sdk/client-s3`, `posthog-js`, `@walletpass/pass-js`
3. **Simplify auth**: Keep email/password, remove Google OAuth provider temporarily
4. **Keep infrastructure**: Database schema pattern, UI components, auth middleware

---
