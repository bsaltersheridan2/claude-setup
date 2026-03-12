# Dependabot Review

Systematically triage and merge dependabot PRs.

## Process

1. **List open dependabot PRs** with CI status
2. **Assess risk** for each:
   - **Low**: devDependency patches (@types/*, linters, test libs)
   - **Medium**: dependency minor versions
   - **High**: major bumps, security advisories, runtime dependencies
3. **Flag for human review**: major bumps, security advisories, runtime changes, breaking changes
4. **Group related packages**: e.g., all `@typescript-eslint/*` together
5. **Merge one at a time** — after each merge, request rebase on remaining: `@dependabot rebase`

## Risk Assessment Table

```
| PR | Package | From → To | Type | Risk | CI |
```

Risk indicators: low, medium, high

## Rules

- NEVER auto-merge high-risk updates without user approval
- Always check changelogs for breaking changes on minor+ bumps
- Verify CI passes before merging
- For Python: check if the update affects any pinned transitive dependencies
