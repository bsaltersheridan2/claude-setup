---
paths:
  - "**/routes/**"
  - "**/routers/**"
  - "**/endpoints/**"
  - "**/api/**"
  - "**/handlers/**"
---

# API Design Conventions

- Use consistent error response shapes across all endpoints.
- Validate input at the boundary — use Pydantic models (Python) or zod schemas (TypeScript).
- Return appropriate HTTP status codes (don't use 200 for errors).
- Use plural nouns for resource endpoints: `/users`, `/orders`.
- Paginate list endpoints by default.
- Include request IDs in error responses for traceability.
- Log errors with context (request ID, user ID, endpoint) — never log request bodies containing PII.
