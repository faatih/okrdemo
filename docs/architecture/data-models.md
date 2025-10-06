# Data Models

Based on PRD requirements and database schema (Story 1.2), the core business entities are:

### Model: Team

**Purpose:** Represents organizational units (e.g., "Direct Channel Sales", "Corporate Sales") that own Objectives and contain Users. Maps to airline S&M org structure.

**Key Attributes:**
- `id`: string (UUID) - Primary key
- `name`: string - Team display name (e.g., "Direct Channel Growth")
- `organizationId`: string (UUID) - Unused in MVP, prepared for multi-tenant Phase 2
- `archived`: boolean - Soft delete flag (hide from UI, preserve data)
- `createdAt`: timestamp - Record creation time
- `updatedAt`: timestamp - Last modification time

**TypeScript Interface:**
```typescript
interface Team {
  id: string;
  name: string;
  organizationId: string | null; // Phase 2: multi-tenant support
  archived: boolean;
  createdAt: Date;
  updatedAt: Date;
}
```

**Relationships:**
- Has many: `User` (team members)
- Has many: `Objective` (team goals)

### Model: User

**Purpose:** Represents individual users (KR owners, team leads, executives). Owns Key Results and Objectives.

**Key Attributes:**
- `id`: string (UUID) - Primary key
- `email`: string - Unique email address
- `name`: string - Full name (e.g., "John Smith")
- `teamId`: string (UUID) - Foreign key to Team
- `organizationId`: string (UUID) - Unused in MVP, prepared for multi-tenant Phase 2
- `active`: boolean - Soft delete flag (deactivated users can't login)
- `createdAt`: timestamp - Record creation time
- `updatedAt`: timestamp - Last modification time

**TypeScript Interface:**
```typescript
interface User {
  id: string;
  email: string;
  name: string;
  teamId: string;
  organizationId: string | null; // Phase 2: multi-tenant support
  active: boolean;
  createdAt: Date;
  updatedAt: Date;

  // Relations (populated via joins)
  team?: Team;
  ownedObjectives?: Objective[];
  ownedKeyResults?: KeyResult[];
}
```

**Relationships:**
- Belongs to: `Team`
- Has many: `Objective` (as owner)
- Has many: `KeyResult` (as owner)
- Has many: `CheckIn` (as creator)

**Note:** Better Auth adds `user`, `session`, `account` tables - preserved for Phase 2 integration but unused in MVP.

### Model: Quarter

**Purpose:** Represents quarterly planning periods (e.g., "2025-Q1"). Objectives are scoped to a Quarter.

**Key Attributes:**
- `id`: string (UUID) - Primary key
- `label`: string - Display label (e.g., "2025-Q1", "Q1 2025")
- `startAt`: date - Quarter start date (e.g., 2025-01-01)
- `endAt`: date - Quarter end date (e.g., 2025-03-31)
- `organizationId`: string (UUID) - Unused in MVP, prepared for multi-tenant Phase 2
- `archived`: boolean - Soft delete flag
- `notes`: text - QBR notes field (Story 3.1)
- `createdAt`: timestamp - Record creation time
- `updatedAt`: timestamp - Last modification time

**TypeScript Interface:**
```typescript
interface Quarter {
  id: string;
  label: string;
  startAt: Date;
  endAt: Date;
  organizationId: string | null; // Phase 2: multi-tenant support
  archived: boolean;
  notes: string | null; // QBR commentary
  createdAt: Date;
  updatedAt: Date;

  // Relations
  objectives?: Objective[];
}
```

**Relationships:**
- Has many: `Objective` (goals for this quarter)

**Business Rules:**
- `endAt` must be after `startAt`
- No overlapping quarters for same organization (Phase 2 validation)
- Default format: "YYYY-QX" but allows custom labels

### Model: Objective

**Purpose:** High-level strategic goals (e.g., "Grow Direct Channel Revenue"). Groups 2-4 Key Results. Maps to OKR "O".

**Key Attributes:**
- `id`: string (UUID) - Primary key
- `title`: string - Objective description (e.g., "Expand Corporate Sales in APAC")
- `teamId`: string (UUID) - Foreign key to Team
- `quarterId`: string (UUID) - Foreign key to Quarter
- `ownerId`: string (UUID) - Foreign key to User (executive owner)
- `organizationId`: string (UUID) - Unused in MVP, prepared for multi-tenant Phase 2
- `createdAt`: timestamp - Record creation time
- `updatedAt`: timestamp - Last modification time

**TypeScript Interface:**
```typescript
interface Objective {
  id: string;
  title: string;
  teamId: string;
  quarterId: string;
  ownerId: string;
  organizationId: string | null; // Phase 2: multi-tenant support
  createdAt: Date;
  updatedAt: Date;

  // Relations
  team?: Team;
  quarter?: Quarter;
  owner?: User;
  keyResults?: KeyResult[];

  // Computed (not stored)
  confidence?: ConfidenceLevel; // Rolled up from KRs
  progressPercent?: number; // Aggregated from KRs
  lastUpdated?: Date; // Most recent CheckIn timestamp
}

type ConfidenceLevel = 0 | 1 | 2; // Red=0, Amber=1, Green=2
```

**Relationships:**
- Belongs to: `Team`, `Quarter`, `User` (owner)
- Has many: `KeyResult` (2-4 typically per PRD guideline)

**Business Rules:**
- PRD suggests 1-3 Objectives per team per quarter (soft limit, UI warning)
- Confidence derived from worst KR confidence (Story 2.5)

### Model: KeyResult

**Purpose:** Measurable outcomes under an Objective (e.g., "Increase premium cabin bookings from 12% to 18%"). Maps to OKR "KR".

**Key Attributes:**
- `id`: string (UUID) - Primary key
- `title`: string - KR description with measurement (e.g., "Premium cabin bookings: 12% → 18%")
- `objectiveId`: string (UUID) - Foreign key to Objective
- `ownerId`: string (UUID) - Foreign key to User (individual contributor)
- `unit`: enum - Measurement type: `'%'`, `'pp'`, `'$'`, `'#'` (PRD FR5)
- `direction`: enum - Target direction: `'up'` or `'down'` (PRD FR6)
- `startValue`: decimal - Baseline value at quarter start
- `targetValue`: decimal - Goal value at quarter end
- `currentValue`: decimal - Latest value from most recent CheckIn
- `createdAt`: timestamp - Record creation time
- `updatedAt`: timestamp - Last modification time

**TypeScript Interface:**
```typescript
type Unit = '%' | 'pp' | '$' | '#';
type Direction = 'up' | 'down';

interface KeyResult {
  id: string;
  title: string;
  objectiveId: string;
  ownerId: string;
  unit: Unit;
  direction: Direction;
  startValue: number;
  targetValue: number;
  currentValue: number;
  createdAt: Date;
  updatedAt: Date;

  // Relations
  objective?: Objective;
  owner?: User;
  checkIns?: CheckIn[];

  // Computed
  progressPercent?: number; // (current - start) / (target - start) * 100
  latestConfidence?: ConfidenceLevel; // From most recent CheckIn
  weeksSinceUpdate?: number; // For "stale KR" detection
}
```

**Relationships:**
- Belongs to: `Objective`, `User` (owner)
- Has many: `CheckIn` (weekly updates)

**Business Rules:**
- PRD suggests 2-4 KRs per Objective (soft limit, UI warning)
- `currentValue` updated from CheckIn saves (Story 2.1)
- For `direction='down'`, progress inverted (lower is better)

### Model: CheckIn

**Purpose:** Weekly updates to KeyResult with new value, confidence, and optional note. Maintains history for trends (sparklines, Risk Rail).

**Key Attributes:**
- `id`: string (UUID) - Primary key
- `krId`: string (UUID) - Foreign key to KeyResult
- `value`: decimal - New measured value for this week
- `confidence`: enum - RAG status: `0` (Red), `1` (Amber), `2` (Green)
- `note`: text - Optional commentary (max 500 chars per PRD FR11)
- `createdBy`: string (UUID) - Foreign key to User (who created this check-in)
- `createdAt`: timestamp - Check-in submission time (used for weekly aggregation)

**TypeScript Interface:**
```typescript
interface CheckIn {
  id: string;
  krId: string;
  value: number;
  confidence: ConfidenceLevel; // 0=Red, 1=Amber, 2=Green
  note: string | null;
  createdBy: string;
  createdAt: Date;

  // Relations
  keyResult?: KeyResult;
  creator?: User;
}
```

**Relationships:**
- Belongs to: `KeyResult`, `User` (creator)

**Business Rules:**
- Immutable after creation (no edits, only undo within 10s via optimistic UI rollback)
- `createdAt` used for weekly bucketing in sparkline calculation (Story 2.4)
- Latest CheckIn updates KeyResult.currentValue (Story 2.1)

### Model: Import

**Purpose:** Tracks CSV import history for auditing and debugging. References created Objectives/KRs for traceability.

**Key Attributes:**
- `id`: string (UUID) - Primary key
- `filename`: string - Original CSV filename
- `rowCount`: integer - Number of rows successfully parsed
- `createdBy`: string (UUID) - Foreign key to User (who imported)
- `createdAt`: timestamp - Import timestamp
- `metadata`: jsonb - Optional: stores parsed data preview, error logs, mapping config

**TypeScript Interface:**
```typescript
interface Import {
  id: string;
  filename: string;
  rowCount: number;
  createdBy: string;
  createdAt: Date;
  metadata: Record<string, any> | null;

  // Relations
  creator?: User;
}
```

**Relationships:**
- Belongs to: `User` (creator)

**Business Rules:**
- Read-only after creation
- PRD limits to 1000 rows max (FR24)

---
