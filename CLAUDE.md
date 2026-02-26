# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A collection of agent skills for personal use. Licensed under MIT.

## Repository Structure

```
skills/
  <skill-name>/
    SKILL.md              # Entry point (required)
    references/           # Supporting material (optional)
```

- Skills live in `skills/<name>/SKILL.md`
- Directory names use kebab-case
- Optional reference files go in `references/`

## Skill Framework

Every skill follows **Canon - Heuristics - Procedure - Artifacts - Gates**:

1. **Canon** — anchors in established literature
2. **Heuristics** — checklist of principles to apply
3. **Procedure** — step-by-step execution workflow
4. **Artifacts** — structured output format
5. **Gates** — quality checks before completion

## Frontmatter

Every `SKILL.md` requires YAML frontmatter with:
- `name`: kebab-case, matches directory name
- `description`: one sentence, starts with "Use when..."
