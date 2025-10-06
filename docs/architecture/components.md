# Components

### Frontend Components

**ObjectiveCard** - Dashboard grid card (Story 2.2)
- **Responsibility:** Display Objective summary with visual indicators
- **Technology Stack:** React + TypeScript, Tailwind CSS, Recharts for sparkline

**BulletBar** - Progress visualization
- **Responsibility:** Show start → current → target with colored progress bar
- **Technology Stack:** React + SVG, Tailwind for colors

**Sparkline** - 6-week trend chart
- **Responsibility:** Render mini line chart from weekly data points
- **Technology Stack:** Recharts, responsive container

**ConfidenceChip** - RAG indicator
- **Responsibility:** Display confidence level with color + icon
- **Technology Stack:** shadcn/ui Badge component, Okabe-Ito colors

**KRRow** - Check-ins inline editor
- **Responsibility:** Editable row for weekly check-in input
- **Technology Stack:** shadcn/ui Input, Select components

### Backend Components

**OKRService** - Business logic layer
- **Responsibility:** OKR creation, confidence rollup, progress calculation
- **Technology Stack:** TypeScript classes, transaction handling

**CheckInService** - Check-in processing
- **Responsibility:** Batch save, currentValue update, sparkline invalidation
- **Technology Stack:** TypeScript, PostgreSQL transactions

**QBRGenerator** - Report generation (Story 3.1)
- **Responsibility:** Generate QBR data from quarter's Objectives/KRs
- **Technology Stack:** SQL aggregations, TypeScript data transformation

---
