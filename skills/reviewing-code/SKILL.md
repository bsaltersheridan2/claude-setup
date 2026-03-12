# Reviewing Code

Automated review-fix-verify cycle for your own code before committing or creating a PR.

## Modes

- **Pre-commit**: Reviews branch diff against main
- **Pre-PR**: Full code review + PR readiness checks

## Process

1. **Launch review agents** via `review-orchestrator` agent (parallel)
2. **For each finding**:
   - Verify with `verified-analysis` skill
   - Classify: VALID / UNCERTAIN / FALSE POSITIVE
   - Fix VALID findings immediately
3. **Run verification** — invoke `verifying` skill after fixes
4. **Repeat** — max 3 review rounds
5. **Write checkpoint** to `~/.claude/reviews/<project>/branch-<name>/checkpoint.md`

## Rules

- Max 3 review rounds — if issues persist after 3, report remaining
- Compact context at round 2+ before re-running agents
- Fix VALID findings, skip FALSE POSITIVE, flag UNCERTAIN for user
