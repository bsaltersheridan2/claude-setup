# Implementing a Linear Issue

Orchestrate end-to-end implementation of a Linear issue.

## Process

1. **Fetch issue** — `mcp__linear-server__get_issue`
2. **Display summary** — show title, description, priority, labels. Get user confirmation.
3. **Update status** — set to "In Progress" via Linear API
4. **Create branch**:
   - Determine prefix from labels: Bug → `fix/`, Feature → `feat/`, Improvement → `chore/`
   - Format: `{prefix}/{TEAM-NUMBER}-{slug}`
5. **Create worktree** — invoke `superpowers:using-git-worktrees`
6. **Implement with TDD** — invoke `superpowers:test-driven-development`
7. **Finish work** — invoke `finishing-work` skill
8. **Create PR** — invoke `creating-pr` skill, use `[TICK-42]` format in title
9. **Update Linear** — set status to "Done"
10. **Link PR** — add comment with PR URL via `mcp__linear-server__create_comment`

## Rules

- EVERY step above marked with "invoke" is REQUIRED — do not skip
- Always confirm with user before starting implementation
- If implementation reveals the issue needs clarification, pause and ask
