---
name: python-guidelines
description: Use when writing, changing, or reviewing Python code. Covers typing, concurrency, performance, and greenfield tooling.
---

# Python Guidelines

Follow the repository's Python version, tooling, and conventions. Use [greenfield defaults](greenfield.md) when starting a project.

- Type function signatures and data boundaries. Let obvious local types be inferred. Use precise collection types and modern annotations supported by the project. Keep necessary `Any` at a narrow boundary.
- Prefer async for concurrent I/O and in existing async applications. Use sequential code when it is sufficient for a small script or command. Keep blocking calls off the event loop when they could stall other work. When a Typer command needs async application code, use a synchronous entry point with `asyncio.run()` unless the project has an established pattern.
- Use human-readable logs by default. Let the application configure logging. Reuse clients and connection pools when their lifecycle makes that worthwhile.
- For slow workloads, measure first. Cut repeated work, batch I/O, and use suitable standard or optimized libraries. Add parallel execution or a native extension only when the measured gain justifies the maintenance cost. Prefer a small PyO3 extension with maturin when Rust is warranted and the project has no other convention.
