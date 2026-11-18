# Skills

A collection of reusable instructions for coding agents. Each skill has a `SKILL.md` that defines when it applies and how to perform the task. A skill directory can also contain supporting reference files.

## Locally maintained skills

| Skill | Purpose |
| --- | --- |
| [`agent-delegation`](agent-delegation/SKILL.md) | Contract for delegating work to agents: required context, references, and the evidence standard for completion. |
| [`coding-guidelines`](coding-guidelines/SKILL.md) | Practical engineering defaults: scope and complexity, change discipline, default stack, error handling, logging, and UI/UX. |
| [`document-guidelines`](document-guidelines/SKILL.md) | Plain-language maintainer documentation and runnable operator guides. |
| [`user-communication`](user-communication/SKILL.md) | Transparent reporting, evidence-based claims, constructive disagreement, and follow-through. |
| [`implementation-review`](implementation-review/SKILL.md) | Independent review contract for a diff or change: boundaries, checks, severity, verdict, and reporting. |
| [`security-review`](security-review/SKILL.md) | Independent security review contract: dependency and supply-chain checks, vulnerability classes, severity, verdict, and reporting. |
| [`python-guidelines`](python-guidelines/SKILL.md) | Python implementation guidelines; [`greenfield.md`](python-guidelines/greenfield.md) adds default dependencies and tooling for new projects. |
| [`visual-review`](visual-review/SKILL.md) | Independent browser-based review of rendered interfaces, responsive layouts, and interaction states, with findings and a verdict. |
| [`x-inspired-frontend-design`](x-inspired-frontend-design/SKILL.md) | A frontend design direction: restrained surfaces, crisp typography, and responsive, accessible layouts across product domains. |
| [`playwright-cli-manual`](playwright-cli-manual/SKILL.md) | Locally maintained command reference for Microsoft's [Playwright CLI](https://github.com/microsoft/playwright-cli). It replaced the upstream skill in this repository. |

## External skills

| Skill | Source and purpose |
| --- | --- |
| [`modern-web-guidance`](modern-web-guidance/SKILL.md) | Snapshot of [Google Chrome's Modern Web Guidance](https://github.com/GoogleChrome/modern-web-guidance), with browser support and web platform guidance. The bundled skill identifies its version as `2026_11_09-5bcc021b`. |

## Using the skills

Choose a skill from the table and read its `SKILL.md` before starting the task. Follow links to supporting files when they apply. For Python work, for example, use `python-guidelines` together with `coding-guidelines`; consult `python-guidelines/greenfield.md` when starting a new project.

To use these files with an agent runtime, follow that runtime's instructions for skill discovery and invocation. The `description` in each skill identifies the tasks it covers.

## Format

Each skill is a directory containing `SKILL.md` with YAML frontmatter:

```yaml
---
name: skill-name
description: When this skill applies, plus what it covers.
---
```

The `name` identifies the skill, and the `description` states when to use it. The current skills use only these two frontmatter fields. Optional supporting files live beside `SKILL.md` and are linked from it; for example, [`python-guidelines/greenfield.md`](python-guidelines/greenfield.md) provides defaults for new Python projects.

## Adding a skill

1. Create one directory per skill, containing a `SKILL.md` with `name` and `description` frontmatter.
2. Make the directory name match the skill name, and state when the skill applies in its description.
3. Keep instructions concise and accurate. Link to supporting files instead of duplicating their content.
4. Keep durable guidance separate from temporary plans, work logs, and debugging notes.
5. Add the skill to the relevant table and check that all relative links resolve. For an imported skill, record the upstream source, version, and license.

## License

The repository's own material uses the [MIT License](LICENSE). The imported `modern-web-guidance` material uses the [Apache License 2.0](modern-web-guidance/LICENSE).
