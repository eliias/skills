---
name: clean-code-review
description: "You MUST use this when reviewing, modifying, or improving existing code for readability and maintainability."
---

# Clean Code Review

## Canonical Lineage

This skill draws from three foundational texts on software craft:

- **Clean Code** (Robert C. Martin) — naming, functions, comments, error handling, and code smells
- **Refactoring** (Martin Fowler) — safe, incremental behavior-preserving transformations
- **Implementation Patterns** (Kent Beck) — expressing intent through code structure

## Operating Definition

Clean code **minimizes cognitive load for the next reader** and **reduces the cost of future change**. Every recommendation from this skill serves one or both of these goals. When readability and cleverness conflict, readability wins.

## Heuristics

See [references/heuristics.md](references/heuristics.md) for the full catalog of code smells, naming rules, function design, comment hygiene, error handling, design principles, and test quality checks.

## Procedure

### Phase 1: Context Scan

1. Read the target files or diff. If invoked on a PR or changeset, focus on changed lines but consider surrounding context.
2. Check for project conventions: linter configs, style guides, `CLAUDE.md`, `CONTRIBUTING.md`, or existing patterns in the codebase.
3. Identify the language, framework, and test setup so recommendations are idiomatic.

### Phase 2: Diagnose

1. Walk through the heuristics catalog against the target code.
2. Record each finding with:
   - **Location**: file and line range
   - **Heuristic violated**: reference from the catalog
   - **Severity**: high (blocks understanding or causes bugs), medium (hinders readability), low (style or minor improvement)
   - **Rationale**: one sentence explaining the impact
3. Rank findings by severity, then by proximity to the change (closer to the diff = higher priority).
4. Drop any finding that contradicts an established project convention.

### Phase 3: Propose

1. For each finding, describe a concrete fix with before/after snippets.
2. Group related findings that can be addressed in a single refactoring step.
3. If a fix is risky or subjective, flag it as **optional** and explain the tradeoff.

### Phase 4: Apply

1. Refactor in small, independently verifiable steps — one conceptual change per step.
2. After each step, confirm the code still compiles or parses (run linter or type checker if available).
3. Commit or checkpoint logically so each step can be reviewed or reverted independently.

### Phase 5: Validate

1. Run the project's test suite. If no tests exist, note this as a finding.
2. Verify no behavioral change was introduced (same inputs produce same outputs).
3. If tests fail after a refactoring step, **revert that step** and report the failure.
4. Run linter/formatter if configured in the project.

## Artifacts

Structure your output as follows:

```
## Summary
One-paragraph overview: what was reviewed, scope, and overall code health assessment.

## Findings

| # | Location | Heuristic | Severity | Description |
|---|----------|-----------|----------|-------------|
| 1 | file:L10-25 | Long method | High | ... |

## Changes Applied

For each change:
### Change N: <title>
- **Finding(s)**: #1, #2
- **What**: brief description
- **Before**: code snippet
- **After**: code snippet

## Validation Results
- Tests: pass/fail (N tests, N passed, N failed)
- Linter: pass/fail
- Behavioral change: none / describe

## Deferred Items
Items not addressed and why (out of scope, needs team discussion, etc.)
```

## Quality Gates

Before marking the review as complete, confirm:

- [ ] Every high-severity finding is addressed or explicitly deferred with rationale
- [ ] Net complexity is reduced (or unchanged if only low-severity items remain)
- [ ] All existing tests pass after changes
- [ ] Each change is small enough to review independently
- [ ] No new warnings introduced by linter or type checker
- [ ] Deferred items are documented with reasoning
