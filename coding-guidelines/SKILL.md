---
name: coding-guidelines
description: Use when planning, writing, changing, or reviewing code. Covers reversible decisions, readable implementation, and house engineering defaults.
---

# Coding Guidelines

## Decisions and scope

- Make routine, reversible decisions using the request and repository conventions. Mention an assumption when it affects the result. Ask only when unresolved uncertainty would materially change the outcome, when a stated boundary would be crossed, or when a decision is costly to undo.
- Skip speculative work. If a credible failure mode warrants extra complexity, weigh its likelihood and impact against the maintenance cost. Keep the change focused and preserve behavior that callers rely on.
- Reuse repository code first. Prefer the standard library or an existing dependency when it fits. Add a dependency when it clearly simplifies the work or provides a capability the project needs.

## Readable, reliable code

- Use names from the problem domain. Make inputs, main steps, and outputs easy to trace. Prefer straightforward control flow and add an abstraction when it makes the job easier to follow. A little duplication can be clearer than a shared abstraction.
- Comment on why a rule or constraint matters. Validate at trust boundaries and let unexpected failures surface clearly. Catch exceptions for useful context, cleanup, recovery, or boundary reporting. A clear error and nonzero exit can suffice for a small script.
- Verify changed behavior through its normal entry point. Match the checks to the impact and realistic failure modes.
- Write logs for people first. Include useful diagnostic context and omit sensitive values. Add structured output when a consumer needs it. Make progress visible during long operations.
- Use familiar terms and units in the UI. Tell users when missing, stale, or estimated data changes how they should interpret a result or what they should do next. Keep implementation details in maintainer docs.

## Greenfield defaults

Use these defaults for the parts the project needs. Follow an established repository stack.

- Frontend — TypeScript, Vite, React, Tailwind CSS
- Backend — Python 3.13+, FastAPI, Pydantic v2+. Add SQLAlchemy and Alembic for relational persistence when needed.
- Database — PostgreSQL 18+ in production. SQLite for local development or tests when compatible.
- CLI — Python 3.13+. Prefer Typer for a non-trivial CLI.
- Redis 8+ and Docker are available choices when the project calls for them.
