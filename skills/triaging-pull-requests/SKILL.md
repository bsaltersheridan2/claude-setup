# Triaging Pull Requests

Triage open PRs by action needed.

## Process

1. **Gather PRs** — `gh pr list --json number,title,author,mergeable,baseRefName,headRefName,statusCheckRollup,reviews,isDraft,createdAt,comments`
2. **Classify each PR** into exactly ONE group (first match wins):
   1. **Blocked** — base branch is another PR's head
   2. **Needs rebase** — mergeable = CONFLICTING
   3. **CI failing** — status checks failing
   4. **Changes requested** — review with CHANGES_REQUESTED
   5. **Needs review** — no approving review
   6. **Ready to merge** — approved + CI passing
   7. **Stale** — no updates in 30+ days

## Output Format

Use 4-column table: `| PR | Title | Author | Detail |`

- Render draft PRs separately
- Terse detail phrases (e.g., "approved, CI passing")
- Include comment count when > 0
- Plain markdown tables (no code fences)

## Summary

Bold one-liner with PR counts per group. Flag dependabot PRs ready to merge.
