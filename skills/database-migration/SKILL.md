# Database Migration

Checklist for writing safe, reversible database migrations.

## Before Writing

1. **Check current schema state** — read the latest migration and models
2. **Identify dependencies** — will this migration affect running queries? Other services?
3. **Plan rollback** — every migration must have a working downgrade path

## Writing the Migration

### Schema Changes
- Add columns as nullable first, backfill, then add NOT NULL constraint in a follow-up
- Never rename columns directly — add new, migrate data, drop old (3-step process)
- Add indexes concurrently where supported (`postgresql_concurrently=True`)
- Keep schema and data migrations in separate files

### Data Migrations
- Process in batches (1000–10000 rows) to avoid locking
- Make idempotent — re-running should be safe
- Include progress logging for long-running migrations
- Test with production-scale data volumes (not just empty tables)

## Testing

1. Run upgrade against a fresh database
2. Run upgrade against a database with existing data
3. Run downgrade and verify it cleanly reverses
4. Verify application code works with both old and new schema (for zero-downtime deploys)

## Deployment Checklist

- [ ] Migration is backward-compatible with current application code
- [ ] Downgrade path tested
- [ ] Estimated runtime for production data volume
- [ ] Backup plan documented
- [ ] Related application code changes are in the same PR (or sequenced correctly)
