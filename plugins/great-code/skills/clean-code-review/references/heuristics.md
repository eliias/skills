# Clean Code Heuristics Reference

A compact catalog of code quality heuristics. Each table lists the smell or principle, a diagnostic question, and the recommended action.

## Code Smells

| Smell | Diagnostic | Action |
|-------|-----------|--------|
| Large class | > 1 clear responsibility? | Split into focused classes |
| Primitive obsession | Passing raw strings/ints that represent a domain concept? | Introduce a value object or type alias |
| Feature envy | Method uses more data from another class than its own? | Move method to the class it envies |
| Data clumps | Same group of parameters passed together repeatedly? | Introduce a parameter object |
| Shotgun surgery | One change requires edits in many unrelated files? | Consolidate related logic into a single module |

## Functions

| Principle | Diagnostic | Action |
|-----------|-----------|--------|
| Do one thing | Can you describe the function without using "and"? | Split into separate functions |
| Command-query separation | Does the function both mutate state and return a value? | Split into a command (void) and a query (return) |
| Descriptive name | Does the name fully describe what the function does? | Rename to match the actual behavior |

## Comments

| Principle | Diagnostic | Action |
|-----------|-----------|--------|
| Explain why, not what | Does the comment restate what the code already says? | Delete it or rewrite to explain *why* |
| No commented-out code | Dead code left behind "just in case"? | Delete it; version control has history |
| No redundant comments | Comment says exactly what the function signature says? | Delete it |
| Clarify intent | Complex algorithm or business rule that is non-obvious? | Add a concise *why* comment |
| TODO with context | Temporary workaround without explanation? | Add `TODO(author): reason` with a tracking reference |

## Error Handling

| Principle | Diagnostic | Action |
|-----------|-----------|--------|
| Exceptions over error codes | Returning -1, null, or status codes for failures? | Throw/raise typed exceptions |
| Context in messages | Error message says "failed" with no detail? | Include what was attempted, what input caused it, and why it failed |
| Don't return null | Caller must null-check every return value? | Return empty collection, Optional, or throw |
| Fail fast | Invalid state detected but execution continues? | Validate at entry and fail immediately |
| Don't ignore exceptions | Empty catch blocks or swallowed errors? | Handle, re-throw, or log with context |
| Use specific exceptions | Catching `Exception` or `Error` broadly? | Catch the narrowest type possible |

## Design

| Principle | Diagnostic | Action |
|-----------|-----------|--------|
| High cohesion | Class methods operate on different subsets of fields? | Split into classes where all methods use all fields |
| Low coupling | Changing one module forces changes in many others? | Introduce interfaces or event-based communication |
| Encapsulation | Internal state accessed directly from outside? | Make fields private, expose behavior not data |
| Dependency inversion | High-level module depends on a concrete low-level detail? | Depend on abstractions (interfaces/protocols) |
| Composition over inheritance | Deep inheritance hierarchy (> 2 levels)? | Refactor to use composition and delegation |
| Law of Demeter | Chaining calls like `a.getB().getC().doThing()`? | Tell, don't ask — move behavior to the appropriate object |
| Open/Closed | Modifying existing code to add every new variant? | Use polymorphism or strategy pattern to extend |

## Tests

| Principle | Diagnostic | Action |
|-----------|-----------|--------|
| One concept per test | Test asserts multiple unrelated things? | Split into focused tests |
| Descriptive names | Test named `test1` or `testFunction`? | Name as `should_<expected>_when_<condition>` |
| Fast | Test suite takes > 10 seconds? | Mock external dependencies, avoid I/O |
| Independent | Tests fail when run in different order? | Remove shared mutable state between tests |
| Readable | Test requires reading the implementation to understand? | Use Arrange-Act-Assert with clear variable names |
| No test logic | Tests contain conditionals or loops? | Tests should be straight-line code |
| Boundary cases | Only happy path tested? | Add tests for edge cases, nulls, empty inputs, and error paths |
