# Triaging Issues

Determine "what should I work on next?" by analyzing GitHub Issues.

## Process

1. **Gather issues** — `gh issue list --state open --json number,title,labels,assignees,createdAt,updatedAt`
   - Include `closedByPullRequestsReferences` to detect issues with active PRs
2. **Filter out**:
   - Issues labeled `wontfix`, `duplicate`, `invalid`
   - Issues with active (open) PRs already addressing them
3. **Detect hierarchy** — check for parent/child via `/repos/{owner}/{repo}/issues/{number}/sub_issues` API
4. **Organize by priority**:
   - Parent groups first (work children before standalone)
   - Then by label tier: Bugs > Features > Maintenance > Needs triage > Uncategorized
5. **Recommend**: First unassigned in highest-populated tier

## Output Format

Use 4-column markdown table: `| Issue | Title | Labels | Assigned |`

Group by parent (if any), then by label tier. Skip on-hold issues with note.

## Summary

Bold one-liner with issue counts per group and a clear recommendation.
