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

## Auto-Invocation

Skills activate automatically via a session-start hook. When the plugin loads, the [using-great-code](plugins/great-code/skills/using-great-code/SKILL.md) meta-skill is injected into the session. It checks each user message against skill triggers and invokes the matching skill without requiring an explicit slash command.

You can still invoke skills manually:

```
/clean-code-review
/refactoring
```

## Skills

| Skill | Description |
|-------|-------------|
| [clean-code-review](plugins/great-code/skills/clean-code-review/SKILL.md) | Review, modify, or improve existing code for readability and maintainability |
| [refactoring](plugins/great-code/skills/refactoring/SKILL.md) | Disciplined two-hat development: alternate between adding function and refactoring |
| [using-great-code](plugins/great-code/skills/using-great-code/SKILL.md) | Meta-skill that auto-invokes other skills when relevant (injected at session start) |

## License

MIT
