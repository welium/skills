---
name: security-review
description: Use when performing an independent security review of code, a change, configuration, or a project's dependencies, or when acting as a security review gate. Defines scope, checks, severity, verdict, and reporting.
---

# Security Review

Review independently for security defects, treating the author's summary and the code's stated intent as untrusted. Inspect the actual implementation, configuration, dependencies, and data flows, and verify claims with evidence.

A review is either advisory or a required gate. When it is a required gate, the verdict governs that workflow. An advisory review does not create an approval gate that was not requested.

## Boundaries

* Review and validate only; do not modify the implementation or tracked content, and do not delegate the assigned review.
* Keep artifacts and caches in a temporary directory, not in the workspace. Routine command execution is allowed; targeted high-risk commands may require approval or be disallowed. Do not bypass these rules or the read-only boundary using wrappers, alternate paths, interpreters, or different command spellings. Permission to run a tool does not authorize work outside the assigned scope.
* Security testing must not attack systems, data, or accounts outside the assigned scope. Do not exfiltrate secrets, and redact sensitive values in findings.
* Apply the project's conventions and any applicable security or language guidelines proportionally to the task.

## Dependencies and Supply Chain

Check dependencies by default, whether or not the change touched them:

* **Known vulnerabilities:** Query CVEs and advisories for direct and transitive dependencies, including unchanged ones. Flag a vulnerable dependency even when the change did not modify it; a known flaw is material regardless of who introduced it.
* **Pinning and currency:** Unpinned ranges, missing or drifted lockfiles, and versions left behind security fixes.
* **Trustworthiness:** Unmaintained or abandoned packages, typosquatting, unexpectedly privileged packages, and install or build scripts that execute on resolve.
* **Actual usage:** Confirm the vulnerable code is actually used and reachable from an untrusted boundary before assigning high severity; state exposure and compensating controls when they materially change the risk.

Use the ecosystem's tooling where available (advisory databases, lockfile auditors, dependency scanners) and record the exact command and result.

## What to Review

Review only materially affected areas, except that known security flaws are always in scope:

* **Secrets and credentials:** Hardcoded secrets, tokens, or keys in source, config, logs, error output, or version-control history; insecure storage; overly broad credentials.
* **Input handling and injection:** SQL/NoSQL/command/template/LDAP/XPath injection, unsafe deserialization, path traversal, SSRF, XSS, CSRF, response splitting, and missing or incorrect validation at trust boundaries.
* **Authentication and authorization:** Session and token handling, credential storage, privilege checks, broken object- and function-level authorization, insecure direct object references, default credentials, and missing rate limiting.
* **Data protection and cryptography:** Sensitive data exposure, weak or misused algorithms, password hashing, randomness, key management, and data in transit and at rest.
* **Configuration and boundaries:** Insecure defaults, debug or verbose modes, permissive CORS, error messages that leak internals, unnecessary privilege, unsafe file permissions, and exposed endpoints or services.
* **Logic and abuse:** Race conditions and TOCTOU, resource exhaustion and denial of service, mass assignment, unsafe redirects, and tenant or boundary isolation.

## Review Discipline

* Distinguish verified vulnerabilities, hypotheses, and hardening suggestions. Support each finding with concrete evidence and the smallest adequate remediation.
* Prefer demonstrated or clearly reachable issues over theoretical ones. State the preconditions and the plausible impact.
* Judge by actual usage, not by flaw class: severity follows reachability from an untrusted boundary. An RCE in code that is never invoked or is not wired to any input is not P0; classify it as P2 (or lower) and state why.
* Do not invent threats or reject work for stylistic preferences. Require controls proportional to the actual exposure and consequences.
* Do not test beyond the assigned scope, and never degrade the availability, integrity, or confidentiality of systems you do not own.
* Stop once there is enough evidence for a reliable verdict. Never claim scans, checks, or results that were not actually performed.

## Severity and Verdict

* **P0 Critical:** Remotely exploitable or otherwise critical flaw with severe impact (code execution, authentication bypass, mass data exposure), or a critical vulnerable dependency in active use.
* **P1 High:** A material vulnerability readily exploitable with serious impact.
* **P2 Medium:** A real weakness with limited impact or meaningful preconditions, or a vulnerable dependency that is not readily exploitable.
* **P3 Low:** Hardening, defense-in-depth, or minor exposure.

Judge severity against actual usage, demonstrated reachability from an untrusted boundary, exploitability, and impact; a flaw that cannot be reached in practice is not critical regardless of its class. Note an existing CVE or advisory identifier, or a CVSS vector, where it adds precision.

State exactly one verdict:

* `APPROVED`: No unresolved P0–P2 security findings remain in the reviewed scope.
* `CHANGES_REQUIRED`: One or more actionable P0–P2 findings remain.
* `BLOCKED`: The target, dependencies, evidence, or environment needed for a reliable verdict are unavailable.

## Reporting

Write the review for a human reader: lead with the verdict and the evidence behind it. There is no fixed template; include what a reader needs to act on and omit boilerplate.

* State what was reviewed: code, configuration, dependencies, data flows, and the tooling or commands actually run.
* List findings in descending severity, each with its location, the evidence, the vulnerability class, the preconditions and impact, and the smallest adequate remediation. Distinguish verified issues from hypotheses.
* Note dependency findings with the package, version, advisory or CVE, and whether it is reachable or directly used.
* State what was not reviewed or could not be verified, and why.
* Never claim checks or scan results that were not actually performed.
