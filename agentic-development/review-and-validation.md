# Agentic Review and Validation Standards

*Companion document in the Agentic Development Standards family*

This document defines independent review, deterministic verification, validation evidence, and truthful reporting for agent-produced work. It is authoritative for the detailed rules in its scope.

## 1. Engineering Standards Remain Applicable

Agent-generated code and artifacts MUST satisfy the same applicable engineering standards as human-generated work.

Use of an agent MUST NOT be treated as evidence that a change has been reviewed, tested, secured, documented, or otherwise validated.

## 2. Deterministic Validation

When available and applicable, deterministic tooling SHOULD be used to execute validation such as:

- Builds and compiler diagnostics
- Unit tests
- Integration tests
- Static analysis
- Linters and format validation
- Schema and data-contract validation
- Database migration validation
- Security or dependency policy checks
- Packaging or deployment validation

An agent MAY interpret failures, design tests, identify missing coverage, or recommend additional validation. It MUST NOT replace required deterministic execution with a statement that the code appears correct.

Validation evidence MUST distinguish executed checks from checks that were unavailable, skipped, inferred, or merely recommended.

An agent MUST NOT fabricate, infer, or report successful test execution when the relevant command or tool did not actually complete successfully.

## 3. Failure Reporting

Failed, incomplete, unavailable, flaky, or inconclusive validation MUST be reported accurately.

A task MUST NOT be represented as fully validated when required checks remain unresolved.

An agent attempting to correct a failure MUST NOT silently delete tests, weaken assertions, disable analyzers, suppress diagnostics, change acceptance criteria, or bypass policy solely to make validation pass.

Changes to validation rules or test expectations MAY be appropriate when the existing rule is incorrect, but such changes MUST be justified and reviewed as changes to the specification or control rather than disguised as implementation fixes.

## 4. Independent Review

Where independent review is required, the producing implementation execution MUST NOT treat its own review as satisfying that requirement.

A Reviewer SHOULD examine the relevant change, requirements, evidence, tests, risks, and applicable standards rather than merely summarize the implementer's explanation.

Review findings SHOULD identify disposition clearly, such as accepted, rejected, changes required, questions requiring resolution, or risks requiring approval.

A reviewer MAY use agent-produced analysis, but independent review MUST preserve the reviewer's ability to disagree and form a separate judgment.

## 5. Risk-Proportionate Validation

Validation depth SHOULD be proportionate to the impact and failure modes of the change.

Changes affecting production infrastructure, authentication, authorization, sensitive data, financial calculations, migrations, destructive operations, public contracts, or other high-impact behavior SHOULD receive validation and review appropriate to those risks.

Trivial documentation or low-risk mechanical changes MAY use lighter review when project policy permits it. Independence requirements SHOULD NOT be applied ceremonially where they add cost without materially reducing risk.

---

[Return to the Agentic Development Standards](../agentic-development.md)
