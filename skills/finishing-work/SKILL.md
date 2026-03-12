# Finishing Work

Process before committing — ensures quality and captures learnings.

## Process

1. **Reflect on session** — identify learnings, corrections, patterns worth codifying
2. **Update docs if needed** — session notes, convention docs, skills
3. **Run verification** — invoke `verifying` skill (REQUIRED — do not skip)
4. **Run code review** — invoke `reviewing-code` with code-reviewer agent (REQUIRED — do not skip)
5. **Commit** — only after verification AND code review pass

## What to Capture in Session Notes

- Architectural decisions and their rationale
- Corrections to AI approach (what was wrong, what's correct)
- Working patterns discovered
- Testing strategies that worked
- Bugs found and their root causes

## Rules

- NEVER commit without running both `verifying` and code review
- Include actual command output evidence in commit message
- Write session notes to `~/.claude/session-notes/<project>/`
- If verification fails, fix before committing — don't commit broken code
