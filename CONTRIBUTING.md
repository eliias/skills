# Contributing

## Skill Framework

Every skill in this repository follows the **Canon - Heuristics - Procedure - Artifacts - Gates** framework:

| Layer | Purpose |
|-------|---------|
| **Canon** | Anchors the skill in established literature or prior art |
| **Heuristics** | Provides a concrete checklist of principles to apply |
| **Procedure** | Defines the step-by-step execution workflow |
| **Artifacts** | Specifies the structured output format |
| **Gates** | Lists quality checks that must pass before completion |

## Directory Structure

```
skills/
  <skill-name>/
    SKILL.md              # Entry point (required)
    references/           # Supporting material (optional)
      heuristics.md
      examples.md
```

- Use **kebab-case** for skill directory names
- `SKILL.md` is always the entry point
- Place reference material in a `references/` subdirectory

## SKILL.md Template

```markdown
---
name: <skill-name>
description: <One sentence. Use when...>
---

# <Skill Title>

## Canonical Lineage
Brief anchor in established sources. Cite books, papers, or prior art.

## Operating Definition
What does this skill optimize for? One paragraph.

## Heuristics
Link to or inline the checklist of principles this skill applies.

## Procedure

### Phase 1: <Name>
Steps...

### Phase 2: <Name>
Steps...

(Add as many phases as needed.)

## Artifacts
Define the structured output format.

## Quality Gates
Checklist of conditions that must be true before the skill is complete.
```

## Frontmatter Requirements

Every `SKILL.md` must include YAML frontmatter with:

- `name` (required): kebab-case identifier matching the directory name
- `description` (required): one sentence starting with "Use when..."

## Adding a New Skill

1. Create `skills/<skill-name>/SKILL.md` following the template above
2. Add reference files in `skills/<skill-name>/references/` if needed
3. Update the skill catalog table in `README.md`
4. Test by symlinking to `~/.claude/skills/` and invoking in Claude Code
