---
name: coding-guidelines
description: Apply when planning, implementing, modifying, or reviewing code.
---

# Coding Guidelines

## Core Principle

Be a practical engineer. Deliver the simplest reliable solution that meets the actual requirements.

Prefer, in order:

1. Existing repository functionality and conventions
2. Standard library
3. Already-installed dependencies
4. Established new dependencies that materially reduce complexity
5. Minimal custom code

## Scope & Complexity

- Follow KISS and YAGNI. Solve real problems only.
- Make the smallest cohesive change. Avoid unrelated refactoring.
- Preserve existing behavior unless explicitly asked to change it.
- Avoid unnecessary abstractions, frameworks, service layers, factories, registries, DI, configuration systems, retries, concurrency, compatibility layers, and recovery mechanisms.
- Prefer fewer moving parts, straightforward control flow, easy debugging, and low maintenance cost.
- Match effort to actual requirements, risks, and failure modes.

## Change Discipline

- Identify the root cause and fix it directly.
- Implement only what is required to satisfy the stated requirements.
- Verify with proportionate tests or checks. Once requirements are met, stop.
- Do not expand scope, "improve" surrounding code, or add speculative features.
- Prefer local, readable edits over broad rewrites.

## Defaults

When the repository does not establish a stack:

- Frontend: TypeScript, Vite, React, Tailwind CSS
- Backend: Python 3.13+, FastAPI, Pydantic v2+, SQLAlchemy, Alembic
- Database: PostgreSQL 18+ (production); SQLite for development/testing when compatible
- CLI: Python 3.13+, Typer
- Optional: Redis 8+, Docker

## Errors & Validation

- Fail clearly. Do not hide unexpected failures.
- Catch exceptions only to recover meaningfully or add useful context.
- Validate at trust boundaries; trust established internal contracts.
- Preserve diagnostic context without exposing sensitive information.
- For small scripts, an uncaught exception and non-zero exit code are often sufficient.

## Code Quality

- Write human-readable code with meaningful names and explicit control flow.
- Comment on non-obvious constraints, trade-offs, and decisions. Avoid restating the code.
- Avoid obvious inefficiencies (N+1 queries, redundant I/O).
- Prefer async/coroutines for I/O-bound work when supported and beneficial.

## UI/UX

- All user-facing text must be meaningful, clean, and professional.
- Never expose implementation details, internal assumptions, data-processing rules, fallback behavior, or developer notes in the UI.
- Handle missing or uncertain data in application logic. Present clean values, placeholders (e.g. "—"), or empty states without explaining the handling.
- Keep technical explanations in code comments or developer documentation only.

## Logging

- Log meaningful events and failures with sufficient diagnostic context, including relevant variable values, field values, identifiers, and error details.
- Use appropriate severity levels and structured, searchable logs.
- Avoid excessive verbosity, redundant messages, and sensitive information. Ordinary identifiers are generally not sensitive.
- For long-running tasks, emit visually distinctive progress logs that are easy for human operators to spot in auto-scrolling output.