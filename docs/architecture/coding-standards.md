# Coding Standards

### Critical Fullstack Rules

- **Type Sharing:** Always define shared types in `types/*.ts` and import from there
- **API Calls:** Never make direct `fetch()` calls - use `lib/api-client.ts` service layer
- **Environment Variables:** Access only through config objects, never `process.env` directly in components
- **Error Handling:** All API routes must use standard error format
- **State Updates:** Never mutate state directly - use proper state management patterns
- **Mock Auth Boundary:** Always use `getCurrentUser()` helper, never hardcode `'user-1'`
- **Database Queries:** Always use Drizzle ORM query builder, never raw SQL
- **Validation:** All API endpoints must validate input with Zod schemas

### Naming Conventions

| Element | Frontend | Backend | Example |
|---------|----------|---------|---------|
| **Components** | PascalCase | - | `ObjectiveCard.tsx` |
| **Hooks** | camelCase with 'use' | - | `useCheckIns.ts` |
| **API Routes** | kebab-case | kebab-case | `/api/check-ins` |
| **Database Tables** | snake_case | snake_case | `key_result` |

---
