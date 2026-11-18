---
name: security-review
description: Use for an independent defensive security review of code, configuration, dependencies, or data flows.
---

# Security Review

Review the actual code, configuration, dependency graph, and data flow. Do the review yourself. Keep tracked content read-only and use non-destructive checks within the assigned scope. Redact sensitive values in findings.

- Identify entry points, privileges, and data crossing trust boundaries. Focus on the risks those paths expose, such as authorization gaps, unsafe input handling, leaked data, and insecure defaults.
- Check advisories for direct and transitive dependencies, including unchanged ones. Start with the relevant applications and lockfiles. Record the tool or source, the installed version, and the advisory ID. Check actual usage and whether untrusted input can reach the affected code.
- Where relevant, check for lockfile drift, unpinned dependencies, questionable package provenance, and install or build hooks that execute code.
- Set severity by demonstrated or clearly supported reachability, preconditions, and impact. An unreachable code-execution flaw can merit follow-up at lower severity. Use P0 for critical, P1 for high, P2 for material, and P3 for minor exposure or hardening. Separate verified findings from hypotheses.

Lead with `APPROVED` if the evidence supports it, `CHANGES_REQUIRED` for actionable material findings, or `BLOCKED` when missing access or evidence prevents a verdict. Gate delivery only when required by the user or workflow. Report evidence, likely impact, a focused remedy, and meaningful coverage gaps.
