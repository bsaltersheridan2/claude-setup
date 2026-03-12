---
paths:
  - "**/migrations/**"
  - "**/alembic/**"
  - "**/*migration*"
---

# Database Migration Conventions

- Every migration MUST be reversible. Include both `upgrade()` and `downgrade()`.
- Never drop columns or tables without a deprecation period — rename first, remove later.
- Use `op.batch_alter_table()` for SQLite compatibility when needed.
- Add indexes concurrently where supported: `op.create_index(..., postgresql_concurrently=True)`.
- Test migrations against a real database, not mocks.
- Data migrations belong in separate migration files from schema migrations.
- Always verify the downgrade path works before merging.
