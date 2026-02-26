# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A plugin marketplace of agent skills for Claude Code. Licensed under MIT.

## Repository Structure

```
.claude-plugin/
  marketplace.json            # Marketplace catalog
plugins/
  great-code/
    .claude-plugin/
      plugin.json             # Plugin manifest
    skills/
      <skill-name>/
        SKILL.md              # Entry point (required)
        references/           # Supporting material (optional)
```

- This repo is a **plugin marketplace** — installable via `/plugin marketplace add eliias/skills`
- Skills live in `plugins/great-code/skills/<name>/SKILL.md`
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
