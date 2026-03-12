# Reviewing PRs

Review someone else's PR with verified findings.

## Process

1. **Gather context** — `gh pr diff`, read changed files, understand the goal
2. **Run parallel review agents**:
   - code-reviewer
   - silent-failure-hunter
   - pr-test-analyzer
   - type-design-analyzer (if diff contains type definitions)
3. **Verify each finding** — use `verified-analysis` skill for every finding
4. **Classify findings**:
   - **Validity**: VALID / UNCERTAIN / FALSE POSITIVE
   - **Severity**: blocking / suggestion / nit
5. **Present to user** — show all findings for per-finding approval before posting
6. **Post review** — single GitHub review via `gh api`, only approved findings

## Rules

- UNCERTAIN findings are NOT posted unless explicitly approved by user
- Never post a review without showing user first
- Store artifacts in `~/.claude/reviews/<project>/pr-<number>/`
- Be constructive — suggest fixes, not just problems
