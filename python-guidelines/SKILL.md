---
name: python-guidelines
description: Python-specific implementation guidelines. Use when implementing, modifying, or reviewing any Python code.
---

# Python Guidelines

Follow the repository's existing Python version, dependencies, tooling, and conventions first. Apply these defaults when the repository does not establish another choice.

## Language and Typing

* Respect the project's `requires-python`. For greenfield projects, prefer the latest stable CPython supported by required dependencies.
* Prefer modern syntax and idioms available in the project's minimum supported Python version.
* Use explicit type annotations for function parameters, return values, and variables.
* Use native generic syntax such as `list[str]`, `dict[str, int]`, and `tuple[int, ...]` instead of legacy `typing.List`, `typing.Dict`, etc.
* Always parameterize collection types.
* Prefer `X | Y` and `X | None` over `Union[X, Y]` and `Optional[X]`.
* Avoid `Any`. Prefer precise unions, protocols, generics, or type variables. If `Any` is genuinely required, keep its scope narrow and document why.

## Async and Concurrency

Use `asyncio` when the workload benefits from concurrent I/O or the surrounding application is already asynchronous.

* Never perform blocking network, filesystem, database, subprocess, or sleep operations directly inside an async context when an appropriate asynchronous API exists.
* Do not introduce async merely because a task performs I/O; straightforward sequential code is preferable when concurrency provides no meaningful benefit.
* Reuse long-lived clients and connection pools when appropriate rather than creating one client per operation.

For Typer commands that need to execute asynchronous application code, keep the CLI entry point synchronous and enter the async application with `asyncio.run()` unless the project already establishes another pattern. Preserve function metadata when wrapping decorated command functions.

## Logging

* Use structured/contextual fields instead of constructing complex log strings manually.
* Use JSON serialization where logs are intended for machine ingestion.
* Do not log secrets or unnecessarily large payloads.
* Libraries should not globally configure application logging.

## Performance

Optimize when performance matters for the actual workload.

Use this escalation order.

### 1. Improve the Python implementation

First eliminate unnecessary work:

* inefficient algorithms or data structures
* repeated computation or allocation
* N+1 database queries
* per-item network, filesystem, or database operations that can be batched or executed concurrently when appropriate
* unnecessary copies or conversions of large data
* loading complete datasets when streaming or chunking is sufficient

Prefer built-ins and standard-library operations implemented efficiently in native code when they fit naturally.

### 2. Use native-backed libraries

Prefer established optimized implementations before writing low-level code.
Depending on the domain, consider NumPy, Polars, PyArrow, or another established native-backed library.
Prefer vectorized and bulk operations when they materially improve performance. Write comments explaining non-obvious optimizations.
Do not introduce a large numerical or dataframe dependency to optimize trivial workloads.

### 3. Use parallel execution when appropriate

Choose the concurrency mechanism according to the workload and runtime rather than assuming one model universally.
Consider:

* `asyncio` for concurrent I/O.
* Threads for blocking I/O or native operations that release the GIL.
* Free-threaded CPython when it is explicitly part of the deployment environment and required dependencies support it.
* `ProcessPoolExecutor` or multiprocessing for CPU-bound work where process isolation and serialization costs are acceptable.
* `InterpreterPoolExecutor` when isolated interpreters provide an appropriate multi-core execution model.
Account for scheduling, serialization, memory duplication, synchronization, and IPC costs before parallelizing work.

### 4. Move proven hotspots to Rust

Consider Rust only when profiling shows a stable CPU-bound hotspot that cannot be solved cleanly through better algorithms, existing native libraries, Numba, or appropriate parallelism.

* Prefer a small isolated extension over rewriting the application.
* Prefer PyO3 with maturin for Python-facing Rust extensions unless the repository establishes another approach.
* Keep Python/Rust boundaries coarse-grained; avoid frequent calls across the boundary for tiny operations.
* Preserve a clear, typed Python API around compiled components.
* Benchmark across the boundary, not just the Rust implementation in isolation.
* Add Rust only when the measured gain justifies additional build, packaging, debugging, and maintenance complexity.

Do not introduce Rust, multiprocessing, free-threading requirements, or similar optimization machinery speculatively.

Remember that network, database, and storage I/O are often the dominant bottlenecks in Python applications and cannot be fixed by optimizing CPU execution.

## More

**Greenfield Project**: [./greenfield.md](./greenfield.md)
