# Development Workflow

### Local Development Setup

```bash
# 1. Install dependencies
npm install

# 2. Set up environment
cp .env.example .env
# Edit .env with DATABASE_URL and other variables

# 3. Initialize database
npx drizzle-kit generate
npx drizzle-kit push
npm run db:seed

# 4. Start development server
npm run dev
```

### Development Commands

```bash
npm run dev              # Start Next.js dev server (Turbopack)
npm run build            # Production build
npm run lint             # Run ESLint
npm run test             # Run Vitest tests
npm run db:generate      # Generate migrations
npm run db:push          # Push schema to database
npm run db:seed          # Seed sample data
npm run db:studio        # Open Drizzle Studio
```

---
