---
name: implementation-review
description: Use for an independent implementation review of code or a diff against stated requirements and project conventions.
---

# Implementation Review

Review the actual diff, affected behavior, and tests against the request and repository conventions. Do the review yourself and keep tracked content read-only. Keep check artifacts temporary. A verdict gates delivery only when the user or workflow requires it.

- Trace the normal entry point and realistic failure paths. Check requirements, existing callers and data, security boundaries, and material regressions. Run relevant checks. A representative run may suffice for a one-off script.
- Flag complexity when it creates a concrete risk or a meaningful maintenance cost. Straight-line code, clear failures, and limited duplication are valid choices. Treat speculative concerns and stylistic preferences as optional unless the project explicitly requires them.

Lead with `APPROVED` when the requirements and checks support it, `CHANGES_REQUIRED` when a material issue remains, or `BLOCKED` when missing evidence prevents a verdict. Rank findings by impact. Use P0 for critical, P1 for high, P2 for material, and P3 for optional follow-up. Give each finding a location, evidence, consequence, and the smallest adequate fix. List checks actually run and meaningful gaps.
