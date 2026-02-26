# Simplicity Heuristics Reference

## Evaluation Dimensions

| Dimension | Diagnostic Question |
|-----------|-------------------|
| Mental hops | How many concepts must a reader hold in memory to follow the main path? |
| Abstraction fitness | Does each abstraction earn its keep with a concrete, current motivation? |
| Locality | Can you understand a piece of code by reading only that piece? |
| Narrative flow | Does the code read top-to-bottom without requiring the reader to jump elsewhere? |
| Essential vs. accidental | Is the complexity in the code proportional to the complexity in the problem? |
| Name-concept alignment | Do names match the domain concepts they represent, at the right level of specificity? |
| Change cost | Would a likely future change be local and predictable, or scattered and risky? |

## Default Heuristics

| Heuristic | Rationale |
|-----------|-----------|
| Prefer clarity over reuse | Duplicated code that is easy to read is better than a shared abstraction that is hard to follow. |
| Prefer locality over indirection | Code that lives near its context is easier to reason about than code reached through layers. |
| Prefer explicit over implicit | State changes, side effects, and control flow should be visible at the call site. |
| Prefer concrete over generic | Start with the specific case. Generalize only when a second concrete case arrives. |
| Prefer linear over branching | A straight execution path is easier to follow than nested conditionals or scattered cases. |
| Prefer fewer concepts over fewer lines | Reducing line count by introducing a new abstraction increases conceptual load. |

## Simplicity Failure Catalog

| Failure | Signal | Why It Hurts |
|---------|--------|-------------|
| Mixed abstraction levels | A function body interleaves high-level orchestration with low-level detail. | The reader cannot skim; they must shift mental gears mid-function. |
| Speculative generality | Type parameters, plugin hooks, or configuration with exactly zero or one consumer. | Abstraction cost is paid now; the benefit may never arrive. |
| Unnecessary indirection | A function that only calls another function. A class that only wraps another class. | Each hop adds one more thing the reader must track. |
| Hidden side effects | A function named as a query that mutates state, or a constructor that triggers I/O. | The reader's mental model diverges from reality without warning. |
| Branch scattering | The logic for one behavior is spread across multiple conditionals in different locations. | To understand one case, the reader must visit many places. |
| Vague naming | Names like `handle`, `process`, `manager`, `data`, `info`, `utils`. | The reader cannot form a mental model without reading the implementation. |
| Generic containers | `Map<String, Object>`, `Any`, untyped dictionaries used to avoid defining a type. | No compile-time guidance; the reader must trace usage to understand shape. |
| Premature DRY | Two code paths merged into one with flags or conditionals to handle their differences. | Coupling unrelated callers makes each change ripple unpredictably. |
| Deep nesting | More than two levels of indentation from conditionals, loops, or callbacks. | Each nesting level multiplies the mental state the reader must track. |
| Temporal coupling | Code that must be called in a specific order but does not enforce that order. | Correct usage depends on convention rather than structure. |

## Simplification Moves

| Move | When to Apply | Effect |
|------|--------------|--------|
| Inline | Abstraction has one call site or adds no conceptual value. | Removes a hop; makes the logic visible in context. |
| Extract for naming | A block of code has a coherent purpose but no name. | Gives the reader a summary without changing structure. |
| Replace conditional with polymorphism | Repeated type-checking switches on the same discriminator. | Collocates each case's logic; removes scattering. |
| Introduce parameter object | Three or more parameters travel together across functions. | Names the concept; reduces argument noise. |
| Flatten nesting | Deep conditionals with early-return opportunities. | Linearizes the main path; makes exceptions visible at the top. |
| Split mixed abstraction | A function mixes orchestration and detail. | Each function operates at one level; the reader can choose depth. |
| Remove speculative code | Abstractions, parameters, or hooks with no current consumer. | Reduces concepts; simplifies the dependency graph. |
| Make side effects explicit | Hidden mutations or I/O inside apparently pure functions. | Aligns the reader's mental model with reality. |
| Collocate scattered logic | One behavior's logic is spread across multiple locations. | The reader finds all relevant code in one place. |
| Replace generic container with named type | Untyped maps or `Any` used as domain objects. | Compile-time guidance; self-documenting shape. |

## Judgment Discipline

Every simplicity judgment must be inspectable — another engineer should be able to challenge it with specific disagreements.

| Rule | Replace | With |
|------|---------|------|
| Convert intuition to claims | "This feels wrong" / "This is elegant" / "This is overengineered" | "This abstraction merges cases that change independently" / "This helper hides control flow without removing complexity" / "This structure reduces duplication while preserving domain distinctions" |
| Require observable evidence | Aesthetic discomfort | One of: mixed abstraction levels, hidden side effects, scattered branching, parameterized behavior flags, vague naming, indirection without compression, speculative reuse, generic containers replacing domain concepts |
| Generate counterarguments | Unchallenged recommendation | "The strongest defense of the current design is X. That defense is/is not sufficient because Y." |
| State limits | Confident verdict | "This judgment assumes Z. If Z is false — for instance if [scenario] — the recommendation would change to W." |
| Classify duplication | "Violates DRY" | One of: accidental (syntax overlap, different domain meaning), essential (true shared logic), currently acceptable (may diverge, keep separate until third case) |

## Pitfalls

| Pitfall | Description |
|---------|------------|
| Simplicity theater | Reducing line count or file count without reducing conceptual load. Fewer lines is not simpler if each line does more. |
| Clarity for the author | Code that is clear to the person who just wrote it but opaque to someone without that context. Test by re-reading after a break. |
| Hiding essential complexity | Making code *look* simple by pushing complexity into convention, implicit behavior, or framework magic. The complexity still exists; it is just invisible. |
| Over-inlining | Removing every abstraction collapses useful conceptual boundaries. Some hops are worth their cost when they name a real concept. |
| Confusing unfamiliar with complex | A pattern may be unfamiliar to you but well-known to the team. Check project conventions before flagging. |
