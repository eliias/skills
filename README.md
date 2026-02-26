# skills

A plugin marketplace of agent skills for Claude Code, built on a structured framework.

## Installation

Install from the marketplace:

```bash
/plugin marketplace add eliias/skills
/plugin install eliias@great-code
```

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
| [clean-code-review](plugins/great-code/skills/clean-code-review/SKILL.md) | Review and refactor code for readability and maintainability |
| [refactoring](plugins/great-code/skills/refactoring/SKILL.md) | Disciplined two-hat development: alternate between adding function and refactoring |

## License

MIT
