# Review PR Feedback

Evaluate review comments on your own PR, apply valid fixes, and respond to reviewers.

## When to Use

- PR has review comments that need triage and response
- User says "review the review", "address PR feedback", "handle review comments"

## Process

1. **Gather context** — find PR, fetch all review comments, read referenced files
2. **Evaluate each comment** using the assessment matrix below
3. **Categorize** each comment into an action
4. **Present summary table** to user before making changes
5. **Apply fixes** for approved items
6. **Draft reply comments** for push-backs and acknowledgements
7. **Post and push** after user approves

## Gathering Comments

```bash
gh pr list --head BRANCH_NAME --json number,title,url
gh api repos/OWNER/REPO/pulls/PR_NUMBER/comments \
  --jq '.[] | {id: .id, author: .user.login, body: .body, path: .path, line: .line}'
```

Read every file referenced by review comments to understand code in context.

## Assessment Matrix

| Dimension | Questions |
|-----------|-----------|
| **Validity** | Is the concern technically correct? Does it apply to this code? |
| **Severity** | Bug? Code smell? Nitpick? Theoretical edge case? |
| **Scope** | In-scope for this PR, or a follow-up? |
| **Conventions** | Does the suggestion match existing codebase patterns? |
| **Effort vs value** | Trivial fix or significant rework? |

## Verification

Use `verified-analysis` skill for any non-obvious claim. Especially:
- "This library behaves like X" — check the docs
- "This pattern causes Y" — trace the execution path
- "This convention is Z" — grep the codebase for existing patterns

## Action Categories

| Action | When |
|--------|------|
| **Apply** | Valid, in-scope, worth fixing now |
| **Push back** | Incorrect, out of scope, over-engineered, or not worth the trade-off |
| **Acknowledge** | Valid but out of scope — note as follow-up |
| **Skip** | Pure nitpick, no meaningful impact |

### Apply signals
- Matches an existing convention the PR missed
- Fixes a real bug (state management, error handling, null safety)
- Trivial to fix and improves quality
- Reviewer has domain expertise

### Push-back signals
- Defensive code for scenarios the library already handles
- Premature abstraction / DRY-ing non-duplicate code
- "Best practice" that doesn't match actual codebase patterns
- Scope creep — belongs in a separate PR

### Acknowledge signals
- Valid production-hardening concern but not blocking
- Would require significant rework unrelated to the PR's purpose
- Applies equally to existing code, not just new changes

## Presentation

Show findings before acting:

```markdown
| # | File | Comment | Verdict | Action |
|---|------|---------|---------|--------|
| 1 | Service.js:42 | Missing error handling | Valid bug | Apply |
| 2 | Controller.js:18 | Extract helper | Over-engineering | Push back |
| 3 | Service.js:90 | Shutdown hooks | Valid, out of scope | Acknowledge |
```

Include brief reasoning for each verdict, especially push-backs.

## Applying Fixes

- Follow codebase conventions (grep for existing patterns)
- Lint changed files
- Commit: `<ticket>: Address PR review feedback`

## Reply Comments

- Lead with agreement before explaining disagreement
- Be concise and professional
- For push-backs: explain why current approach is sufficient
- For acknowledgements: note value and confirm as follow-up

```bash
gh api repos/OWNER/REPO/pulls/PR_NUMBER/comments \
  -f body="REPLY_TEXT" \
  -F in_reply_to=COMMENT_ID
```

## Rules

- Never apply changes without showing user the evaluation first
- Verify reviewer claims using `verified-analysis` before accepting
- Check codebase conventions before accepting "best practice" suggestions
- Fix everything you accept — don't half-apply feedback
- Post replies and push only after user approval
