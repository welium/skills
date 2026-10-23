---
name: document-guidelines
description: Apply when creating, updating, or reviewing documentation.
---

# Document Guidelines

* Follow ASD-STE100 standard for all documents, with the emphasis below.

## Core Principle

Write accurate, concise, and practical documentation for its intended audience.

* Prioritize information that helps readers understand, use, operate, or maintain the project.
* Keep information consistent with the actual implementation. Do not invent behavior, interfaces, commands, or capabilities.
* Prefer clear explanations, meaningful examples, and straightforward structure over exhaustive descriptions.
* Intended audience is **human** and don't assume native language proficiency. Use clear, simple language.

## Documentation

Durable maintainer documentation describes the **current intended state of the project**, not the session that produced it. The rules below apply to that documentation, not execution plans or work logs.

* Keep durable behavior, architecture, interfaces, configuration, constraints, and operational knowledge.
* Remove scratch notes, debugging trails, failed attempts, temporary workarounds, and superseded designs unless intentionally retained as project history.
* Do not mention conversations, agents, prompts, tool calls, or session-specific implementation history.
* Write for a maintainer arriving with no knowledge of how the current state was produced.
* Prefer final facts and important rationale over implementation narrative.
* Update existing documentation instead of appending a chronological change log unless explicitly required.

A useful test: if a statement will not help a new maintainer six months from now, remove or rewrite it.

Execution plans and work logs may record progress, validation commands and results, agent review evidence, decisions, deviations, blockers, and attempted fixes. Keep them separate from durable documentation and normally untracked unless the user or repository explicitly requires versioning them.

## Operational Handbook / Guides

* Write actionable, self-contained instructions in execution order.
* State prerequisites, environment requirements, and required permissions when not obvious.
* Provide commands in runnable, copy-pasteable code blocks.
  - Avoid placeholders, manual modifications, or adjustments after copying.
  - When customization is unavoidable, isolate it in clearly identified variables or separate manual steps.
* Explain significant side effects, especially destructive or irreversible operations, before the relevant commands.
* Include verification steps and expected outcomes where useful, so operators can determine whether an operation succeeded.
* Keep commands, paths, configuration examples, and procedures consistent with the actual project.