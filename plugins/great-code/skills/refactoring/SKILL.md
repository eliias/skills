---
name: refactoring
description: "You MUST use this when actively developing code to enforce disciplined hat-switching between adding function and refactoring."
---

# Refactoring (Two Hats)

## Canonical Lineage

This skill is grounded in Martin Fowler's *Refactoring* (with Kent Beck, Jay Fields, Shane Harvie):

- **Refactoring** (noun): a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior.
- **Refactoring** (verb): restructuring software by applying a series of refactorings without changing its observable behavior.
- **The Two Hats** (Kent Beck): at any moment you are either *adding function* or *refactoring* — never both. You swap hats frequently, but you always know which one you're wearing.

Supporting sources: *Clean Code* (Martin), *Implementation Patterns* (Beck), *Working Effectively with Legacy Code* (Feathers).

## Operating Definition

This skill enforces a disciplined rhythm during active development: **write code that works, then make it clean — in small, safe steps**. Every coding session alternates between the *adding function* hat (new behavior, new tests) and the *refactoring* hat (restructure, no new behavior, no new tests unless interfaces change). The test suite is the safety net that makes the hat-switching safe.

## Heuristics

See [references/catalog.md](references/catalog.md) for the full refactoring catalog with smell-to-refactoring mappings.

### When to Switch to the Refactoring Hat

- **Before adding function**: understand the code, restructure to make the change easy, then make the easy change
- **After getting a test green**: the code works — now clean it up before moving on
- **Rule of Three**: first time just do it, second time wince, third time refactor
- **During code review or bug fixing**: understanding code is a refactoring opportunity
- **When the code smells**: see the smell catalog — any smell is a signal

### When NOT to Refactor

- Code is so broken it needs a rewrite, not restructuring
- Very close to a hard deadline — take on the technical debt consciously
- No tests exist for the area you'd refactor — write tests first, then refactor

### The Rhythm

1. Ensure tests pass (green)
2. Make one small structural change
3. Run tests again (must stay green)
4. Repeat

Each refactoring step must be small enough that if tests break, you know exactly which change caused it. If a step breaks tests, **revert immediately** rather than debugging forward.

## Procedure

### Phase 1: Assess (Wearing Neither Hat)

1. Read the target code or diff. Understand the change you need to make.
2. Check for a test suite. If tests are missing or insufficient for the area you'll touch, note this — writing tests comes first.
3. Identify the language, framework, and project conventions.
4. Run the existing test suite to establish the green baseline.

### Phase 2: Prepare the Ground (Refactoring Hat)

Before adding new function, restructure existing code to make the change easy:

1. Scan for smells in the area you'll modify (use the smell → refactoring reference).
2. For each smell found, select the appropriate refactoring from the catalog.
3. Apply refactorings one at a time:
   - Make one structural change
   - Run tests — must stay green
   - If tests break, revert the step immediately
4. Stop when the code is clean enough that your intended change has an obvious home.

**Constraint**: No new behavior. No new tests (unless an interface changed and an existing test needs updating). You are only restructuring.

### Phase 3: Add Function (Adding Function Hat)

1. Write a failing test for the new behavior.
2. Write the simplest code to make it pass.
3. Run the full test suite — all green.
4. If you notice the new code is messy, **don't fix it yet**. Note it and switch hats in Phase 4.

**Constraint**: No restructuring. You're adding capability. Resist the urge to clean up mid-implementation.

### Phase 4: Clean Up (Refactoring Hat)

1. Review the code you just wrote. Does it smell?
2. Apply refactorings to integrate the new code cleanly:
   - Extract methods for clarity
   - Rename for intent
   - Remove duplication introduced by the new code
   - Simplify conditionals
3. Each refactoring: change, test, green. One at a time.
4. Run the full test suite after all cleanup.

**Constraint**: No new behavior. All tests must continue to pass.

### Phase 5: Repeat or Complete

1. If more function is needed, return to Phase 3.
2. If the code is clean and all tests pass, proceed to validation.
3. Each cycle should be short — minutes, not hours.

### Phase 6: Validate

1. Run the full test suite. All tests must pass.
2. Run linter/formatter if configured.
3. Review the overall diff: does every change either add tested behavior or improve structure?
4. Ensure no refactoring step accidentally changed behavior (same inputs → same outputs).
5. If any test failed during refactoring and was not cleanly reverted, investigate and fix.

## Artifacts

Structure your output as follows:

```
## Summary
One-paragraph overview: what function was added, what refactoring was performed, overall assessment.

## Hat Log

| # | Hat | Action | Scope | Tests |
|---|-----|--------|-------|-------|
| 1 | Refactoring | Extracted `calculate_total` from `process_order` | order.py:L15-40 | Green |
| 2 | Adding Function | Added discount calculation with test | order.py, test_order.py | Green |
| 3 | Refactoring | Renamed `calc` → `apply_discount_rate` | order.py:L22 | Green |

## Smells Addressed

| Smell | Location | Refactoring Applied |
|-------|----------|-------------------|
| Long Method | order.py:process_order | Extract Method |
| Duplicated Code | cart.py:L10, order.py:L30 | Extract Class |

## Validation Results
- Tests: pass/fail (N tests, N passed, N failed)
- Linter: pass/fail
- Behavioral change: only intended new function / none from refactoring steps

## Deferred Items
Items not addressed and why (out of scope, needs tests first, needs team discussion, etc.)
```

## Quality Gates

Before marking the work as complete, confirm:

- [ ] Every refactoring step preserved existing behavior (tests stayed green throughout)
- [ ] New function is covered by tests
- [ ] No refactoring and function-adding happened in the same step
- [ ] Each change in the hat log is small enough to review independently
- [ ] Smells in the modified area are addressed or explicitly deferred with rationale
- [ ] All tests pass after the final change
- [ ] No new warnings introduced by linter or type checker
- [ ] Deferred items are documented with reasoning
