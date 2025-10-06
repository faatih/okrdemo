# Error Handling Strategy

### Error Response Format

```typescript
interface ApiError {
  error: {
    code: string;           // VALIDATION_ERROR, NOT_FOUND, etc.
    message: string;        // User-friendly message
    details?: any;          // Validation details
    timestamp: string;      // ISO 8601
    requestId: string;      // UUID for tracing
  };
}
```

### Frontend Error Handling

- API client catches all errors
- Display toast notifications
- Rollback optimistic updates on failure

### Backend Error Handling

- Zod validation errors → 400 status
- Service errors → 4xx/5xx status
- Unexpected errors → 500 with sanitized message
- All errors logged to Vercel Logs

---
