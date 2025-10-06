# Testing Strategy

### Testing Pyramid

```
       E2E Tests (Manual for MVP)
      /                          \
     Integration Tests (API Routes)
    /                              \
   Unit Tests (Services, Utils)
```

### Test Organization

**Frontend Tests:**
- Component rendering tests (React Testing Library)
- Custom hooks tests
- Utility function tests

**Backend Tests:**
- Unit tests: Business logic (OKR service, confidence rollup, QBR generator)
- Integration tests: API routes with test database

**Test Framework:** Vitest for all tests (unit + integration)

---
