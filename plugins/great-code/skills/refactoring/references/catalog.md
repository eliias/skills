# Refactoring Catalog

A distilled catalog of refactorings organized by intent category, with smell-to-refactoring mappings. Based on Martin Fowler's *Refactoring*.

## Smell → Refactoring Quick Reference

| Smell | Primary Refactorings |
|-------|---------------------|
| Duplicated Code | Extract Method, Extract Class, Pull Up Method, Form Template Method |
| Long Method | Extract Method, Replace Temp with Query, Introduce Parameter Object, Decompose Conditional, Replace Method with Method Object |
| Large Class | Extract Class, Extract Subclass, Extract Module |
| Long Parameter List | Replace Parameter with Method, Preserve Whole Object, Introduce Parameter Object |
| Divergent Change | Extract Class (one class changed for multiple reasons → split by concern) |
| Shotgun Surgery | Move Method, Move Field, Inline Class (one change touches many classes → consolidate) |
| Feature Envy | Move Method, Extract Method (then move) |
| Data Clumps | Extract Class, Introduce Parameter Object, Preserve Whole Object |
| Primitive Obsession | Replace Data Value with Object, Replace Type Code with Polymorphism/State-Strategy, Extract Class |
| Switch/Case Statements | Replace Conditional with Polymorphism, Replace Type Code with State/Strategy |
| Parallel Inheritance Hierarchies | Move Method, Move Field (collapse one hierarchy) |
| Lazy Class | Inline Class, Collapse Hierarchy |
| Speculative Generality | Collapse Hierarchy, Inline Class, Remove Parameter, Rename Method |
| Temporary Field | Extract Class, Introduce Null Object |
| Message Chains | Hide Delegate, Extract Method, Move Method |
| Middle Man | Remove Middle Man, Inline Method, Replace Delegation with Hierarchy |
| Inappropriate Intimacy | Move Method, Move Field, Extract Class, Hide Delegate, Replace Inheritance with Delegation |
| Alternative Classes with Different Interfaces | Rename Method, Extract Module, Move Method |
| Data Class | Move Method (move behavior into the data class), Encapsulate Collection, Remove Setting Method |
| Refused Bequest | Replace Inheritance with Delegation, Push Down Method |
| Comments (as deodorant) | Extract Method, Rename Method, Introduce Assertion |

## Composing Methods

Refactorings that restructure method bodies for clarity.

| Refactoring | When to Apply |
|-------------|--------------|
| Extract Method | Code fragment that can be grouped; method too long; need to name a concept |
| Inline Method | Method body is as clear as the name; too much indirection |
| Inline Temp | Temp assigned once from a simple expression and gets in the way |
| Replace Temp with Query | Temp holds result of an expression; extract to method for reuse |
| Introduce Explaining Variable | Complex expression is hard to read; break into named parts |
| Split Temporary Variable | Temp assigned more than once (not a loop/collecting var) |
| Remove Assignments to Parameters | Code assigns to a parameter; use a local variable instead |
| Replace Method with Method Object | Long method with many temps that prevent extraction; turn into its own class |
| Substitute Algorithm | Replace a method body with a clearer algorithm |

## Moving Features Between Objects

Refactorings that redistribute responsibilities across classes.

| Refactoring | When to Apply |
|-------------|--------------|
| Move Method | Method uses more features of another class than its own |
| Move Field | Field is used more by another class |
| Extract Class | One class doing the work of two; fields and methods cluster into subgroups |
| Inline Class | Class isn't doing enough to justify its existence |
| Hide Delegate | Client calls through an object to reach a delegate |
| Remove Middle Man | Class has too many delegating methods; just expose the delegate |

## Organizing Data

Refactorings that restructure how data is represented.

| Refactoring | When to Apply |
|-------------|--------------|
| Self Encapsulate Field | Direct field access is causing coupling issues between subclasses |
| Replace Data Value with Object | Data item that needs additional behavior or data |
| Change Value to Reference | Many equal instances that should be a single object |
| Change Reference to Value | Reference object is small, immutable, and hard to manage |
| Replace Array with Object | Array where elements mean different things |
| Replace Magic Number with Symbolic Constant | Literal number with special meaning |
| Encapsulate Collection | Method returns a collection; return a read-only view instead |
| Replace Type Code with Polymorphism | Type code affects behavior; use subclasses |
| Replace Type Code with State/Strategy | Type code affects behavior but class can't be subclassed |
| Replace Subclass with Fields | Subclasses vary only in constant-returning methods |

## Simplifying Conditional Expressions

Refactorings that untangle complex conditional logic.

| Refactoring | When to Apply |
|-------------|--------------|
| Decompose Conditional | Complex conditional (if/then/else) with involved conditions or branches |
| Consolidate Conditional Expression | Sequence of conditionals with the same result; combine and extract |
| Consolidate Duplicate Conditional Fragments | Same code in all branches of a conditional; move outside |
| Remove Control Flag | Variable acting as a control flag for a series of boolean expressions |
| Replace Nested Conditional with Guard Clauses | Method has conditional behavior that doesn't make clear the normal path |
| Replace Conditional with Polymorphism | Conditional that chooses behavior based on type |
| Introduce Null Object | Repeated null checks for the same object; use a null-behavior object |
| Introduce Assertion | Code assumes something about state; make it explicit |

## Making Method Calls Simpler

Refactorings that clarify interfaces and APIs.

| Refactoring | When to Apply |
|-------------|--------------|
| Rename Method | Method name doesn't reveal its purpose |
| Add Parameter | Method needs more information from its caller |
| Remove Parameter | Parameter is no longer used by the method body |
| Separate Query from Modifier | Method both returns a value and changes state |
| Parameterize Method | Several methods do similar things with different hardcoded values |
| Replace Parameter with Explicit Methods | Method behavior is controlled entirely by a parameter value |
| Preserve Whole Object | Pulling several values from an object to pass as parameters |
| Replace Parameter with Method | Object can get the value by calling a method itself |
| Introduce Parameter Object | Group of parameters that naturally go together |
| Remove Setting Method | Field should be set at creation time and never altered |
| Hide Method | Method isn't used outside its class |
| Replace Constructor with Factory Method | Need more than simple construction (e.g., creation based on type code) |
| Replace Error Code with Exception | Method returns a special code to indicate an error |
| Replace Exception with Test | Exception thrown for a condition the caller could check first |

## Dealing with Generalization

Refactorings that restructure inheritance and module hierarchies.

| Refactoring | When to Apply |
|-------------|--------------|
| Pull Up Method | Methods with identical results on subclasses; move to superclass |
| Push Down Method | Behavior on a superclass relevant only to some subclasses |
| Extract Module | Two classes share common behavior; extract a shared module |
| Inline Module | Module doesn't do enough to justify its existence |
| Extract Subclass | Class has features used only in some instances |
| Collapse Hierarchy | Superclass and subclass are not very different |
| Form Template Method | Subclass methods perform similar steps in same order; generalize |
| Replace Inheritance with Delegation | Subclass uses only part of the superclass interface |
| Replace Delegation with Hierarchy | Many delegating methods; hierarchy is simpler |

## Big Refactorings

Strategic refactorings that reshape system architecture over time.

| Refactoring | When to Apply |
|-------------|--------------|
| Tease Apart Inheritance | Inheritance hierarchy doing two jobs at once |
| Convert Procedural Design to Objects | Procedural-style code in an OO language |
| Separate Domain from Presentation | Business logic tangled with UI code |
| Extract Hierarchy | Class doing too much work with many conditionals |
