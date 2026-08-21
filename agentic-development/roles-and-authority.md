# Agentic Roles and Authority Standards

*Companion document in the Agentic Development Standards family*

This document defines logical engineering roles, delegated authority, separation of duties, and human authority boundaries. It is authoritative for the detailed rules in its scope.

## 1. Logical Roles

Agentic workflows SHOULD define responsibilities as logical roles rather than assuming one model or process per responsibility.

A single human may perform several logical roles, and a single agent execution MAY perform more than one compatible role when the resulting authority remains explicit and required independence is preserved.

Common roles include:

- **Coordinator / Orchestrator** — routes work, tracks state, applies workflow policy, and coordinates handoffs.
- **Planning / Architecture** — analyzes requirements, proposes designs, identifies constraints, and records material design decisions.
- **Implementation** — creates or modifies code, configuration, migrations, documentation, tests, and related artifacts within assigned scope.
- **Reviewer** — independently evaluates changes, evidence, risks, conformance, and unresolved defects.
- **Research** — gathers and evaluates external or project evidence needed for a technical decision.
- **Testing / Validation** — executes or designs validation appropriate to the change and reports actual results.
- **Provisioning / Environment Management** — performs approved changes to tools, environments, infrastructure, or privileged configuration.
- **Human Approver / Authority** — makes decisions or grants exceptions reserved to accountable human authority.

An implementation does not need every role. The required roles and separation depend on task risk, impact, and workflow maturity.

## 2. Authority Boundaries

Each role MUST operate only within authority explicitly delegated to that role or execution.

A role's responsibility does not automatically grant every capability that could help it fulfill that responsibility.

For example:

- An Implementation role MAY identify a required tool but MUST NOT infer authority to install it.
- A Research role MAY recommend a dependency but MUST NOT treat the recommendation as approval.
- A Provisioning role MAY install an approved dependency but MUST NOT invent the approval that authorizes installation.
- A Coordinator MAY route a request to an authorized decision-maker but MUST NOT silently grant itself authority reserved for that decision-maker.

Authority SHOULD be narrow enough that an unintended or incorrect action is bounded by the role's actual purpose.

## 3. Separation of Duties

Role separation SHOULD be used where it materially reduces risk, conflicts of interest, or false assurance.

An Implementation role SHOULD NOT independently approve its own material changes when independent review is required by project policy, risk level, or existing standards.

An agent's self-review MAY improve work quality, but MUST NOT be represented as independent review.

Where approval, review, or validation must be independent, the reviewing authority MUST have enough separation from the producing execution to form its own judgment. Separation MAY be provided by another qualified agent execution, deterministic policy, an authorized human, or a combination appropriate to the risk.

A workflow MUST NOT create ceremonial separation in which a nominal reviewer merely repeats or accepts the implementation agent's conclusion without examining the relevant evidence.

## 4. Human Authority

Human approval SHOULD be reserved for meaningful decision boundaries such as:

- Granting new or exceptional authority
- Accepting material security, compliance, licensing, operational, or architectural risk
- Approving production-impacting or difficult-to-reverse actions when required by project policy
- Resolving ambiguity that policy intentionally reserves for accountable judgment
- Overriding an agent or automated recommendation

Routine actions already authorized by explicit policy SHOULD NOT require repeated human approval merely because an agent performs them.

An authorized human MAY override an agent, research, security, or policy recommendation when permitted by applicable higher-level requirements. The override MUST be explicit and MUST record the rationale or accepted risk.

## 5. Delegation Changes

Authority expansion MUST be deliberate. A task discovering that it needs broader access MUST trigger an authority request or escalation rather than silently widening the role.

Temporary authority SHOULD expire when its purpose ends. Privileged, production, or exceptional authority SHOULD be separately scoped and revocable.

A change in role, task, environment, repository, data classification, or policy context SHOULD trigger re-evaluation when the existing delegation may no longer be sufficient or appropriate.

---

[Return to the Agentic Development Standards](../agentic-development.md)
