# Database Schema

### Drizzle Schema Definition

```typescript
// db/schema.ts
import { pgTable, uuid, varchar, text, boolean, timestamp, integer, numeric, date, jsonb } from 'drizzle-orm/pg-core';

export const team = pgTable('team', {
  id: uuid('id').defaultRandom().primaryKey(),
  name: varchar('name', { length: 120 }).notNull(),
  organizationId: uuid('organization_id'), // Phase 2: multi-tenant
  archived: boolean('archived').notNull().default(false),
  createdAt: timestamp('created_at').notNull().defaultNow(),
  updatedAt: timestamp('updated_at').notNull().defaultNow(),
});

export const okrUser = pgTable('okr_user', {
  id: uuid('id').defaultRandom().primaryKey(),
  email: varchar('email', { length: 255 }).notNull().unique(),
  name: varchar('name', { length: 120 }).notNull(),
  teamId: uuid('team_id').notNull().references(() => team.id),
  organizationId: uuid('organization_id'), // Phase 2: multi-tenant
  active: boolean('active').notNull().default(true),
  createdAt: timestamp('created_at').notNull().defaultNow(),
  updatedAt: timestamp('updated_at').notNull().defaultNow(),
});

export const quarter = pgTable('quarter', {
  id: uuid('id').defaultRandom().primaryKey(),
  label: varchar('label', { length: 50 }).notNull(),
  startAt: date('start_at').notNull(),
  endAt: date('end_at').notNull(),
  organizationId: uuid('organization_id'), // Phase 2: multi-tenant
  archived: boolean('archived').notNull().default(false),
  notes: text('notes'), // QBR notes
  createdAt: timestamp('created_at').notNull().defaultNow(),
  updatedAt: timestamp('updated_at').notNull().defaultNow(),
});

export const objective = pgTable('objective', {
  id: uuid('id').defaultRandom().primaryKey(),
  title: varchar('title', { length: 255 }).notNull(),
  teamId: uuid('team_id').notNull().references(() => team.id),
  quarterId: uuid('quarter_id').notNull().references(() => quarter.id),
  ownerId: uuid('owner_id').notNull().references(() => okrUser.id),
  organizationId: uuid('organization_id'), // Phase 2: multi-tenant
  createdAt: timestamp('created_at').notNull().defaultNow(),
  updatedAt: timestamp('updated_at').notNull().defaultNow(),
});

export const keyResult = pgTable('key_result', {
  id: uuid('id').defaultRandom().primaryKey(),
  title: varchar('title', { length: 500 }).notNull(),
  objectiveId: uuid('objective_id').notNull().references(() => objective.id, { onDelete: 'cascade' }),
  ownerId: uuid('owner_id').notNull().references(() => okrUser.id),
  unit: varchar('unit', { length: 5 }).notNull(), // %, pp, $, #
  direction: varchar('direction', { length: 5 }).notNull(), // up, down
  startValue: numeric('start_value', { precision: 15, scale: 2 }).notNull(),
  targetValue: numeric('target_value', { precision: 15, scale: 2 }).notNull(),
  currentValue: numeric('current_value', { precision: 15, scale: 2 }).notNull(),
  createdAt: timestamp('created_at').notNull().defaultNow(),
  updatedAt: timestamp('updated_at').notNull().defaultNow(),
});

export const checkIn = pgTable('check_in', {
  id: uuid('id').defaultRandom().primaryKey(),
  krId: uuid('kr_id').notNull().references(() => keyResult.id, { onDelete: 'cascade' }),
  value: numeric('value', { precision: 15, scale: 2 }).notNull(),
  confidence: integer('confidence').notNull(), // 0=Red, 1=Amber, 2=Green
  note: varchar('note', { length: 500 }),
  createdBy: uuid('created_by').notNull().references(() => okrUser.id),
  createdAt: timestamp('created_at').notNull().defaultNow(),
});

export const importRecord = pgTable('import_record', {
  id: uuid('id').defaultRandom().primaryKey(),
  filename: varchar('filename', { length: 255 }).notNull(),
  rowCount: integer('row_count').notNull(),
  createdBy: uuid('created_by').notNull().references(() => okrUser.id),
  createdAt: timestamp('created_at').notNull().defaultNow(),
  metadata: jsonb('metadata'),
});
```

**Indexes for Performance:**
- `team_org_idx`: team(organization_id)
- `user_team_idx`: okr_user(team_id)
- `obj_quarter_idx`: objective(quarter_id)
- `obj_team_idx`: objective(team_id)
- `kr_obj_idx`: key_result(objective_id)
- `kr_owner_idx`: key_result(owner_id)
- `checkin_kr_idx`: check_in(kr_id)
- `checkin_created_idx`: check_in(created_at)

---
