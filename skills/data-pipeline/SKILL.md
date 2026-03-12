# Data Pipeline

Checklist for building reliable ETL/data pipeline steps.

## Design Principles

1. **Idempotent** — re-running produces the same result (use upserts, not inserts)
2. **Observable** — log progress, record metrics, alert on failure
3. **Resumable** — track progress so failures don't require full re-run
4. **Schema-aware** — validate input/output shapes at boundaries

## Before Writing

1. **Understand the data** — sample the source, check volume, identify edge cases
2. **Define the contract** — input schema, output schema, transformation rules
3. **Plan for failure** — what happens when source is unavailable? Data is malformed?

## Implementation

### Extract
- Validate source connectivity before starting
- Handle pagination/batching for large datasets
- Log record counts at each stage
- Use checksums or watermarks for incremental loads

### Transform
- Validate input records against expected schema
- Handle bad records explicitly: skip with logging, quarantine, or fail-fast
- Never silently drop records
- Use typed models (Pydantic/dataclass) for intermediate representations

### Load
- Use upserts (INSERT ON CONFLICT / MERGE) for idempotency
- Batch writes for performance (1000–5000 rows per batch)
- Verify record counts after load: extracted == transformed == loaded (± expected drops)
- Use transactions for atomicity where appropriate

## Testing

1. **Unit tests**: Transform logic with known input → expected output
2. **Integration tests**: Full pipeline against test database with sample data
3. **Edge cases**: Empty input, malformed records, duplicate records, null values
4. **Idempotency test**: Run pipeline twice, verify same result

## Monitoring Checklist

- [ ] Pipeline duration tracked
- [ ] Record counts logged (extracted, transformed, loaded, skipped, errored)
- [ ] Alerting on: failure, zero records processed, duration > threshold
- [ ] Data quality checks post-load (row counts, null rates, value distributions)
- [ ] Dead letter queue or error log for bad records
