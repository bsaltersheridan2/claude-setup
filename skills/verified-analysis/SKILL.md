# Verified Analysis

Rules for evaluating whether a claim about code is true.

## Confidence Gate

Before classifying any finding, you must prove:
1. **WHAT** is wrong — specific code location and behavior
2. **WHY** it's wrong — reference to spec, convention, or invariant violation
3. **WHAT** the correct behavior should be — concrete fix or expected state

## Tool Selection by Claim Type

| Claim Type | Right Tool |
|-----------|-----------|
| "This code does X" | Read the full function |
| "This framework behaves like Y" | docs-researcher agent |
| "This path leads to Z" | Trace execution with code-explorer |
| "This doesn't exist" | Grep the codebase (MUST grep before asserting absence) |
| "This config does W" | Read the actual config file |

## Evidence Standards

- **Docs confirmation**: Must include version number
- **Execution path**: Must trace from entry point to the relevant line
- **Test proof**: Must show actual test output
- **Grep confirmation**: Must show the grep command and results

## Classification

- **VALID**: All 3 confidence gate checks pass with evidence
- **UNCERTAIN**: Some evidence exists but gaps remain
- **FALSE POSITIVE**: Evidence contradicts the claim

## Rules

- NEVER trust obvious-looking claims without evidence
- Grep before asserting absence — "I didn't see it" is not proof
- Read full functions — snippets can be misleading
- Verify claimed values against actual source
