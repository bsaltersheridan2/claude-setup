# API Design

Checklist for designing and implementing API endpoints.

## Design Phase

1. **Define the contract first** — request/response shapes before implementation
2. **Choose the right HTTP method**: GET (read), POST (create), PUT (replace), PATCH (partial update), DELETE (remove)
3. **Use plural nouns** for resource endpoints: `/users`, `/orders`
4. **Plan error responses** — consistent shape across all endpoints:
   ```json
   {
     "error": {
       "code": "VALIDATION_ERROR",
       "message": "Human-readable description",
       "details": [{"field": "email", "issue": "Invalid format"}],
       "request_id": "req_abc123"
     }
   }
   ```

## Implementation

### Input Validation
- Validate at the boundary — Pydantic models (Python) or zod schemas (TypeScript)
- Return 400 with specific field-level errors
- Sanitize strings to prevent injection

### Authentication & Authorization
- Verify auth before any business logic
- Return 401 for missing/invalid credentials, 403 for insufficient permissions
- Never leak information in auth error messages (don't say "user not found" vs "wrong password")

### Pagination
- Default pagination on all list endpoints
- Use cursor-based pagination for large datasets
- Include `total`, `next_cursor`, `has_more` in response

### Performance
- Set appropriate cache headers
- Use database indexes for filtered/sorted queries
- Add request timeout handling

## Testing Checklist

- [ ] Happy path returns correct status code and shape
- [ ] Invalid input returns 400 with field-level errors
- [ ] Missing auth returns 401
- [ ] Insufficient permissions returns 403
- [ ] Not found returns 404
- [ ] Pagination works correctly (first page, middle, last, empty)
- [ ] Rate limiting behaves correctly (if applicable)
