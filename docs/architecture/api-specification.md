# API Specification

RunwayOKR uses **REST API** with JSON request/response format. All API routes follow Next.js API Routes convention: `app/api/[resource]/route.ts`.

### REST API Specification (OpenAPI 3.0)

```yaml
openapi: 3.0.0
info:
  title: RunwayOKR API
  version: 1.0.0
  description: REST API for airline S&M OKR tracking system
servers:
  - url: http://localhost:3000/api
    description: Local development
  - url: https://okrdemo.vercel.app/api
    description: Production (Vercel)

components:
  securitySchemes:
    mockAuth:
      type: apiKey
      in: header
      name: X-Mock-User
      description: MVP Phase 1 - Mock user ID (always 'user-1')
    betterAuth:
      type: http
      scheme: bearer
      description: Phase 2 - Better Auth session token

  schemas:
    Error:
      type: object
      required:
        - error
      properties:
        error:
          type: object
          required:
            - code
            - message
            - timestamp
            - requestId
          properties:
            code:
              type: string
              example: VALIDATION_ERROR
            message:
              type: string
              example: Invalid input data
            details:
              type: object
              additionalProperties: true
            timestamp:
              type: string
              format: date-time
            requestId:
              type: string
              format: uuid

paths:
  /health:
    get:
      summary: Health check endpoint
      tags: [System]
      responses:
        '200':
          description: Service healthy

  /okrs/create:
    post:
      summary: Create Objectives and Key Results from wizard
      tags: [OKRs]
      description: Story 1.7 - Wizard Step 3 submission
      responses:
        '201':
          description: OKRs created successfully

  /check-ins:
    post:
      summary: Save check-ins (batch)
      tags: [CheckIns]
      description: Story 2.1 - Batch save with optimistic UI
      responses:
        '201':
          description: Check-ins saved successfully

security:
  - mockAuth: []  # Phase 1
```

_(Full OpenAPI spec available in codebase documentation)_

---
