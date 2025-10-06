# Backend Architecture

### Service Architecture (Serverless)

**Function Organization:**
```
app/api/
├── health/route.ts
├── teams/
│   ├── route.ts                # GET, POST
│   └── [id]/route.ts           # PATCH, DELETE
├── okrs/
│   ├── route.ts                # GET
│   ├── create/route.ts         # POST
│   └── [id]/
│       ├── route.ts            # GET, PATCH
│       └── sparkline/route.ts  # GET
├── check-ins/route.ts          # GET, POST
├── reviews/[quarterId]/route.ts
└── imports/parse/route.ts
```

### Data Access Layer (Repository Pattern)

**Repository Classes:**
- `OKRRepository`: Objective and KeyResult queries
- `UserRepository`: User management
- `QuarterRepository`: Quarter CRUD

**Benefits:**
- Decouples business logic from ORM
- Enables unit testing with mocks
- Centralizes database query logic

---
