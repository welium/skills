# Skills

A collection of agent skills. Each skill is a self-contained folder with a `SKILL.md` that an agent runtime loads when its description matches the task at hand, or when it is invoked directly.

## Skills

| Skill | Purpose |
| --- | --- |
| [`agent-delegation`](agent-delegation/SKILL.md) | Contract for delegating work to agents: required context, references, and the evidence standard for completion. |
| [`coding-guidelines`](coding-guidelines/SKILL.md) | Practical engineering defaults: scope and complexity, change discipline, default stack, error handling, logging, and UI/UX. |
| [`document-guidelines`](document-guidelines/SKILL.md) | How to write durable documentation and operator guides, and where execution plans and work logs belong. |
| [`implementation-review`](implementation-review/SKILL.md) | Independent review contract for a diff or change: boundaries, checks, severity, verdict, and reporting. |
| [`security-review`](security-review/SKILL.md) | Independent security review contract: dependency and supply-chain checks, vulnerability classes, severity, verdict, and reporting. |
| [`python-guidelines`](python-guidelines/SKILL.md) | Python implementation guidelines; [`greenfield.md`](python-guidelines/greenfield.md) adds default dependencies and tooling for new projects. |
| [`visual-review`](visual-review/SKILL.md) | Independent review contract for a rendered user interface: inspection approach, discipline, verdict, and reporting. |
| [`x-inspired-frontend-design`](x-inspired-frontend-design/SKILL.md) | A frontend design direction: restrained surfaces, crisp typography, and responsive, accessible layouts across product domains. |
| [`playwright-cli-manual`](playwright-cli-manual/SKILL.md) | Reference manual for the `playwright-cli` browser automation command, with the command list and short examples. |

## Format

Each skill is a directory containing `SKILL.md` with YAML frontmatter:

```yaml
---
name: skill-name
description: When this skill applies, plus what it covers.
---
```

The `description` is the trigger: the runtime matches it against the task to decide whether to load the skill. Supporting files (for example `python-guidelines/greenfield.md`) live beside `SKILL.md` and are referenced from it. Frontmatter uses only `name` and `description`.

## Adding a skill

* Create one directory per skill, containing a `SKILL.md`.
* Make the `description` state when the skill applies.
* Keep it concise and accurate, and prefer referencing other files over duplicating content.
* Keep durable guidance separate from session-specific notes.

## License

Released under the [MIT License](LICENSE).
