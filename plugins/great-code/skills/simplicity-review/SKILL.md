---
name: simplicity-review
description: "Use when evaluating code clarity, questioning abstractions, or investigating overengineering concerns."
---

# Simplicity Review

## Canonical Lineage

This skill synthesizes three perspectives on simplicity in software:

- **Simple Made Easy** (Rich Hickey) — the distinction between *simple* (not interleaved) and *easy* (familiar, nearby). Complexity is objective and measurable by counting entanglements; ease is subjective.
- **The Wrong Abstraction** (Sandi Metz) — "duplication is far cheaper than the wrong abstraction." Prefer inline clarity over premature DRY.
- **Implementation Patterns** (Kent Beck) — code communicates intent to the next reader. Every pattern choice carries a message about what matters.

The core synthesis: good code is *simple* (few entanglements between concepts) and *clear* (the reader reconstructs the author's intent quickly). Simplicity is structural; clarity is narrative. Both are required.

## Heuristics

See [references/heuristics.md](references/heuristics.md) for evaluation dimensions, default heuristics, a simplicity failure catalog, simplification moves, and pitfalls.

## Procedure

### Phase 1: Reconstruct Intent

1. Read the target code without judgment. Identify what the code is *trying to do* — the problem it solves, the domain concepts involved, the main execution path.
2. Note where your understanding stalls. These stall points are signal, not noise.

### Phase 2: Reconstruct the Change Model

1. Determine what kinds of future changes the code is most likely to undergo.
   - Where is variability expected? Which parts are stable?
   - Are there known upcoming requirements, or is extensibility speculative?
2. Assign confidence to each scenario. Do not reward abstractions built only for hypothetical reuse.

### Phase 3: Separate Complexity

1. Classify each area of complexity as **essential** (inherent to the problem domain) or **accidental** (introduced by the implementation).
2. For essential complexity, ask: is the code *clarifying* it or *hiding* it? Hidden essential complexity is a defect.
3. For accidental complexity, ask: what design choice introduced it? Was there a simpler alternative?

### Phase 4: Challenge Abstractions

1. For each abstraction (class, interface, generic type, indirection layer, configuration), ask:
   - Does it have exactly one concrete motivation today, or is it speculative?
   - If removed, how much code would need to change?
   - Does it *separate* concerns or merely *relocate* them?
2. Evaluate abstraction fitness: too abstract (generic containers, over-parameterized) or too concrete (leaking implementation details).

### Phase 5: Identify Failures

1. Walk the heuristics failure catalog against the code.
2. Record each finding with:
   - **Location**: file and line range
   - **Failure type**: from the catalog
   - **Mental hop cost**: how many concepts the reader must hold simultaneously
   - **Rationale**: one sentence explaining why this makes the code harder than the problem

### Phase 6: Propose Moves

1. For each finding, select a concrete simplification move from the catalog.
2. Describe the move with before/after sketches.
3. Flag any move that trades simplicity for other qualities (performance, extensibility) and note the tradeoff explicitly.
4. For each recommendation, articulate the strongest plausible defense of the current design. Why might this code exist as-is? What risk might it be managing? Under what conditions would the current structure be justified?

### Phase 7: Validate

1. Re-read the proposed changes as a coherent whole.
2. Confirm the main execution path is now shorter or more linear.
3. Confirm that no essential complexity was hidden by the changes.
4. Assess risk: are the proposed moves safe and local, or do they cascade?
5. State assumptions and limits: what context is missing, what could invalidate the judgment, what team conventions might change the recommendation.

## Artifacts

Structure your output as follows:

```
## Simplicity Judgment
One paragraph: overall assessment. Is the code simpler than, equal to, or more complex than the problem it solves? State who the judgment applies to (new maintainer, domain expert, original author) and under what change model.

## Complexity Sources (ranked)

| # | Location | Type | Essential/Accidental | Mental Hops | Description |
|---|----------|------|---------------------|-------------|-------------|
| 1 | file:L10-25 | Mixed abstraction levels | Accidental | 3 | ... |

## Suspect Abstractions

| Abstraction | Motivation | Fitness | Recommendation |
|-------------|-----------|---------|----------------|
| ConfigFactory | Speculative | Over-abstract | Inline; extract only if second use appears |

## Proposed Moves

For each move:
### Move N: <title>
- **Finding(s)**: #1, #2
- **Move type**: from catalog
- **Before**: code sketch
- **After**: code sketch
- **Risk**: low/medium/high — explanation

## Counterarguments
For each major recommendation, the strongest defense of the current design and why that defense is or is not sufficient.

## Assumptions & Limits
What context is missing, what assumptions were made, and under what conditions the recommendation would change.

## Risk Notes
Any cross-cutting concerns, cascading changes, or tradeoffs the developer should weigh.
```

## Quality Gates

Before marking the review as complete, confirm:

- [ ] Mental hops are reduced for the main execution path
- [ ] The main path is clearer — a new reader follows it without detours
- [ ] Proposed changes make future modifications safer and more local
- [ ] Essential complexity is clarified, not hidden
- [ ] No move introduces accidental complexity that rivals what it removes
- [ ] Every judgment is backed by structural evidence, not aesthetic preference
- [ ] Counterarguments are stated for each major recommendation
- [ ] Assumptions and missing context are declared
