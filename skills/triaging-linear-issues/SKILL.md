# Triaging Linear Issues

Analyze open Linear issues and recommend work.

## Process

1. **Identify team** — `mcp__linear-server__list_teams`
2. **Fetch issues** — `mcp__linear-server__list_issues` (open state)
3. **Group by priority**: Urgent (1) > High (2) > Medium (3) > Low (4) > No priority (0)
4. **Sort within groups**: Unassigned first → oldest first
5. **Recommend**: Walk tiers top-down, pick first unassigned in highest tier

## Output Format

Markdown tables (plain, no code fences).
Columns: `| Issue | Title | Labels | Age | Assigned |`

Omit empty groups.

## Summary

Bold one-liner with count breakdown per priority tier. Offer to implement recommended issue.
