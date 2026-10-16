---
name: agent-delegation
description: Use when delegating tasks to agents. Provides contract for delegation, context, references, and evidence standards.
---
## Delegation Contract

Delegate in **English**.
Every delegation must be self-contained: state the overall goal, origin and reason for delegation, completed/decided work, the specific owned outcome, boundaries, and validation requirements. Use this structure, additional section could be added as needed:

```markdown
# Task
State one coherent, specific outcome owned by this agent.

# Context
Explain the source request/plan/issue/reviewer result, exact locations, phase and objective when relevant, current status, prior work/findings, decisions, assumptions, and dependencies. A filepath alone is insufficient.

# Constraints
State scope, compatibility, safety restrictions, prohibited operations, unchanged files, and preserved behavior.

# Details
Give relevant paths/symbols, plan or documentation locations, covered acceptance criteria, conventions, required validation, actionable findings, evidence, and output format.

```

References may point to larger sources, but must summarize relevant portions. Before delegating, ensure the message answers: larger outcome, origin, why next, completed work, exact responsibility, what to avoid, and how completion is verified. Never require reconstruction from conversation history.

## Context, Reference, and Instruction Rules

- Identify referenced work by location and meaning. Plan references include filepath, phase number/title, objective, acceptance criteria, and status.
- Reviewer references include reviewed implementation/phase, verdict, actionable findings, and resolved findings. Summarize prior agent conclusions.
- Pass filenames and symbols rather than copied contents unless a tiny excerpt is essential.
- Use imperative, outcome-oriented language; define boundaries without micromanaging.
- Do not include fenced implementation code, combine unrelated outcomes, or use supervisor-only shorthand. Copy actionable reviewer findings into repair briefs and require concrete evidence.

## Evidence Standard

Never accept “done” or “works” alone. Require evidence appropriate to the delegated task: applicable files changed, tests added/updated, exact commands, test/type-check/lint/build/runtime results, diff summary, and assumptions/limitations. For research-only tasks, require sources, findings, and limitations rather than implementation artifacts. Include reviewer verdicts when review was performed; require approval only when the user or workflow establishes a review gate. If validation cannot run, mark it unverified and explain exactly why.
