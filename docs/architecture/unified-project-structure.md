# Unified Project Structure

```
okrdemo/
├── app/                        # Next.js App Router
│   ├── dashboard/              # Pages
│   ├── okrs/
│   ├── check-ins/
│   ├── reviews/
│   ├── imports/
│   ├── settings/
│   ├── api/                    # API Routes (Serverless)
│   ├── layout.tsx
│   ├── page.tsx
│   └── globals.css
├── components/
│   ├── ui/                     # shadcn/ui (existing)
│   ├── okr/                    # OKR domain components
│   ├── wizard/                 # CSV import wizard
│   └── shared/
├── db/
│   ├── drizzle.ts
│   ├── schema.ts
│   └── seed.ts
├── lib/
│   ├── auth/
│   │   ├── auth.ts             # Better Auth config (Phase 2)
│   │   └── mock-session.ts     # Phase 1 mock
│   ├── services/               # Business logic
│   ├── repositories/           # Data access
│   ├── validators/             # Zod schemas
│   ├── utils/
│   └── api-client.ts
├── hooks/
├── types/                      # Shared TypeScript types
├── public/
├── tests/
├── .env
├── drizzle.config.ts
├── next.config.ts
├── package.json
├── tailwind.config.ts
└── tsconfig.json
```

---
