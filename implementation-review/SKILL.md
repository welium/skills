---
name: implementation-review
description: Use when performing an independent implementation review of a diff, change, or code against requirements and conventions, or when acting as a review gate. Defines review boundaries, checks, severity, verdict, and reporting.
---

# Implementation Review

Review independently against explicit requirements, acceptance criteria, and project conventions. Inspect the actual implementation, diff, affected behavior, and relevant tests; do not trust the author's summary alone.

A review is either advisory or a required gate. When it is a required gate, the verdict governs that workflow. An advisory review does not create an approval gate that was not requested.

## Boundaries

* Review and validate only; do not modify the implementation or tracked project content, and do not delegate the assigned review.
* Keep temporary validation artifacts and caches out of the repository and in a temporary directory when possible. Routine command execution is allowed; targeted high-risk commands may require approval or be disallowed. Do not bypass these rules or the read-only boundary using wrappers, alternate paths, interpreters, or different command spellings. Permission to run a tool does not authorize work outside the assigned scope.
* If a check would modify the implementation or tracked content, report the limitation instead of running it, and state who can run it.
* Apply the project's conventions and any applicable coding or language guidelines proportionally to the task.

## Review Checks

Review only materially affected areas:

* **Requirements and correctness:** Verify each acceptance criterion, main success paths, realistic edge cases, data integrity, and visible failures. Reject silently swallowed failures; require exception handling only for meaningful recovery, context, cleanup, or boundary reporting.
* **Security:** Check real trust boundaries for secrets, injection, path traversal, unsafe deserialization, authentication/authorization defects, sensitive data exposure, unnecessary privilege, and missing input validation.
* **Regression and compatibility:** Check preserved behavior and interfaces, incomplete migrations, and directly affected stale documentation.
* **Performance:** Look for material algorithmic inefficiency, repeated computation or I/O, N+1 queries, excessive memory use, blocking operations in async code, leaks, or unbounded concurrency. Do not reject clear code for hypothetical scale or negligible differences.
* **Maintainability and scope:** Check naming, visible control flow, useful comments and contracts, reuse of adequate existing capabilities, and unnecessary dependencies or abstractions. Flag unrelated refactoring and speculative functionality; small duplication is acceptable when it is clearer.
* **Validation:** Assess important behavior, realistic failure paths, and regression coverage. Run relevant checks when practical. Do not demand tests that merely restate the implementation or add disproportionate infrastructure.

## Review Discipline

* Distinguish verified defects, hypotheses, and optional improvements. Support findings with concrete evidence and the smallest adequate correction.
* Do not invent requirements or reject work for personal preferences. Require complexity only for a concrete benefit or realistic failure mode.
* A representative documented execution may suffice for a one-off script. Reusable or production code should normally have automated coverage of important behavior and failures, with security and operational safeguards proportional to actual consequences.
* Accept straightforward sequential code, clear exceptions or non-zero exits, and limited duplication when they are adequate. Do not require elaborate recovery, redundant internal validation, or premature abstractions.
* Stop once there is enough evidence for a reliable verdict. Never claim checks or results that were not actually performed.

## Severity and Verdict

* **P0 Critical:** The change cannot work, breaks deployment or data, or introduces a critical security vulnerability.
* **P1 High:** A material correctness, security, compatibility, or architectural defect that can cause serious failure.
* **P2 Medium:** A real bug, meaningful performance defect, important missing validation or test, or maintainability issue likely to cause future errors.
* **P3 Low:** Non-blocking style, polish, documentation, or optional improvement.

Judge severity against actual evidence and consequences. Treat complexity as P2 only when it materially increases defect risk, operational burden, or maintenance cost; otherwise treat useful simplification as P3.

State exactly one verdict:

* `APPROVED`: All requirements are met, validation is adequate, and no unresolved P0–P2 findings remain. P3 findings may remain.
* `CHANGES_REQUIRED`: One or more actionable P0–P2 findings remain.
* `BLOCKED`: Missing requirements, evidence, environment, dependencies, or access prevent a reliable verdict.

Do not approve merely because work is mostly correct, and do not withhold approval for speculative concerns or non-blocking preferences. When a review is a required gate, a rejected change must be corrected and resubmitted.

## Reporting

Write the review for a human reader: lead with the verdict and the evidence behind it. There is no fixed template; include what a reader needs to act on and omit boilerplate.

* Open with the verdict, then state the files or diff and behavior reviewed, and how each explicit requirement or acceptance criterion fared—met, unmet, or unverified—with brief evidence.
* List findings in descending severity, each with its location, the evidence, the impact, and the smallest adequate correction. Distinguish verified defects from hypotheses.
* State which checks were actually run and their results, and what was not reviewed or could not be verified, and why.
* Keep non-blocking observations and optional simplifications separate from blocking findings.
* Never claim checks or results that were not actually performed.
