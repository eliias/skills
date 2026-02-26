---
name: using-great-code
description: "Meta-skill that auto-invokes great-code skills when relevant. Injected at session start."
---

# Using Great Code Skills

You have the **great-code** plugin installed. It provides specialized skills for writing and maintaining high-quality code. You MUST check these skills before taking action on any user request and invoke the relevant skill when it applies.

## Decision Flow

For every user message, before acting:

1. Read the skill descriptions below.
2. If the user's request matches a skill's trigger, announce which skill you are using and follow it exactly.
3. If multiple skills apply, use the most specific one for the current action.
4. If no skill applies, proceed normally.

## Available Skills

### simplicity-review

**Triggers**: evaluating code clarity, questioning abstractions, overengineering concerns, readability at line/block level, code feels harder than the problem it solves.

Use when the question is "is this code simpler and clearer than it could be?"

Invoke with: `/simplicity-review`

### clean-code-review

**Triggers**: PR reviews, design smell audits, error handling reviews, test quality assessments, module-level structural improvements.

Use when the question is "is this code structurally sound for long-term maintenance?"

Invoke with: `/clean-code-review`

### refactoring

**Triggers**: actively developing code — adding features, fixing bugs, implementing changes that touch existing code. Enforces the two-hat discipline (adding function vs. refactoring).

Use when actively developing code to enforce disciplined hat-switching between adding function and refactoring.

Invoke with: `/refactoring`

## Rules

- Always announce: "Using great-code skill: **<skill-name>**" before following a skill's procedure.
- Follow the skill's full procedure, artifacts format, and quality gates exactly.
- Do not skip quality gates. They exist to catch mistakes.
- If a skill does not apply, do not force it. Proceed with your best judgment.
