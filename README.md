# skills

A collection of agent skills for Claude Code, built on a structured framework.

## Framework

Each skill follows the **Canon - Heuristics - Procedure - Artifacts - Gates** pattern:

- **Canon**: Grounded in established literature and prior art
- **Heuristics**: Concrete checklist of principles to apply
- **Procedure**: Step-by-step execution workflow
- **Artifacts**: Structured output format
- **Gates**: Quality checks that must pass before completion

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full template and guidelines.

## Skills

| Skill | Description |
|-------|-------------|
| [clean-code-review](skills/clean-code-review/SKILL.md) | Review and refactor code for readability and maintainability |

## Installation

Symlink or copy a skill directory into your Claude Code skills folder:

```bash
ln -s $(pwd)/skills/clean-code-review ~/.claude/skills/clean-code-review
```

## License

MIT
