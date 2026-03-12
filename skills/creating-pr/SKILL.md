# Creating a PR

## Process

1. **Run code review FIRST** — invoke `reviewing-code` skill before creating the PR
2. **Extract ticket from branch name** — e.g., `feat/MAIN-1234-add-auth` → `MAIN-1234`
3. **Create the PR**:
   - Title format: `[TICKET-123] Description` (or plain description if no ticket)
   - Body: summary of changes, testing done, any migration notes
   - Use `gh pr create`
4. **Monitor CI** — poll `gh pr checks` every 30 seconds, 15-minute timeout
5. **Report status** — share PR URL and CI outcome

## Rules

- NEVER create a PR without running `reviewing-code` first
- NEVER guess deploy/preview URLs — wait for CI to provide them
- Include migration instructions in PR body if there are schema changes
- Tag relevant reviewers if known
- If CI fails, diagnose before asking user what to do
