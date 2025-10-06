# Security and Performance

### Security Requirements

**Frontend Security:**
- CSP Headers for XSS prevention
- React auto-escaping, DOMPurify for user content
- Session tokens in HTTP-only cookies (Phase 2)

**Backend Security:**
- Zod validation on all API routes (PRD NFR10)
- Rate limiting on import/export endpoints (PRD NFR11)
- Drizzle ORM parameterized queries (SQL injection prevention)
- CORS: same-origin only

**Authentication Security (Phase 2):**
- HTTP-only, Secure, SameSite=Lax cookies
- Better Auth session rotation, 30-day expiry
- bcrypt password hashing with 12 rounds (PRD NFR9)

### Performance Optimization

**Frontend Performance:**
- Bundle Size Target: <300KB initial JS
- SSR for Dashboard (fast first paint)
- Code splitting for wizard steps
- React Query caching (5 min stale time)

**Backend Performance:**
- Response Time Target: <500ms p95
- Database indexes on all foreign keys
- Connection pooling via Neon (max 10)
- No `SELECT *` in production queries

**Performance Budgets:**
- Dashboard load: <2s on 3G (PRD NFR1)
- Check-in save: <500ms (PRD NFR2)
- CSV import (100 rows): <5s (PRD NFR3)
- QBR generation: <3s (PRD NFR4)
- Lighthouse Performance: 90+ (PRD NFR5)

---
