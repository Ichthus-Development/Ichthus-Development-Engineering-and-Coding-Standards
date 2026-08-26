# Agentic Roles and Authority Standards

*Companion document in the Agentic Development Standards family*

This document defines logical engineering roles, delegated authority, separation of duties, coordinator neutrality, and human authority boundaries. It is authoritative for the detailed rules in its scope.

## 1. Logical Roles

Agentic workflows SHOULD define responsibilities as logical roles rather than assuming one model or process per responsibility.

A single human may perform several logical roles, and a single agent execution MAY perform more than one compatible role when the resulting authority remains explicit and required independence is preserved.

Common roles include:

- **Coordinator / Orchestrator** — routes work, tracks state, applies workflow policy, coordinates handoffs, and preserves material competing conclusions without deciding them merely by preference.
- **Planning / Architecture** — analyzes requirements, proposes designs, identifies constraints, and records material design decisions.
- **Implementation** — creates or modifies code, configuration, migrations, documentation, tests, and related artifacts within assigned scope.
- **Reviewer** — independently evaluates changes, evidence, risks, conformance, and unresolved defects.
- **Research** — gathers and evaluates external or project evidence needed for a technical decision.
- **Testing / Validation** — executes or designs validation appropriate to the change and reports actual results.
- **End-User Simulation / Usability Challenge** — exercises user-facing workflows from the perspective of plausible users who do not share the development team's implementation knowledge or assumptions, with emphasis on discoverability, unexpected-but-reasonable behavior, and user-facing failure modes. See [End-User Simulation and Usability](user-simulation-and-usability.md).
- **Adversarial Security Testing** — attempts to identify exploitable behavior, trust-boundary failures, unsafe hostile-input handling, or other security weaknesses within explicitly authorized scope and environments.
- **Independent Challenge** — evaluates whether a prevailing conclusion, framing, design choice, or shared assumption has a credible evidence-based reason to be reconsidered. This role is not required to disagree.
- **Provisioning / Environment Management** — performs approved changes to tools, environments, infrastructure, or privileged configuration.
- **Human Approver / Authority** — makes decisions or grants exceptions reserved to accountable human authority.

An implementation does not need every role. The required roles and separation depend on task risk, impact, uncertainty, irreversibility, and workflow maturity.

Logical roles do not require separate agent processes. A human, a separate execution of the same model, or a distinct model MAY fulfill a role when the required authority and independence are preserved appropriately.

## 2. Authority Boundaries

Each role MUST operate only within authority explicitly delegated to that role or execution.

A role's responsibility does not automatically grant every capability that could help it fulfill that responsibility.

For example:

- An Implementation role MAY identify a required tool but MUST NOT infer authority to install it.
- A Research role MAY recommend a dependency but MUST NOT treat the recommendation as approval.
- An Adversarial Security Testing role MAY identify that broader testing would be valuable but MUST NOT expand its target scope, privileges, environment, or tooling authority without explicit authorization.
- An Independent Challenge role MAY recommend reconsideration but MUST NOT treat the existence of an alternative as authority to redesign or refactor the implementation.
- A Provisioning role MAY install an approved dependency but MUST NOT invent the approval that authorizes installation.
- A Coordinator MAY route a request to an authorized decision-maker but MUST NOT silently grant itself authority reserved for that decision-maker.

Authority SHOULD be narrow enough that an unintended or incorrect action is bounded by the role's actual purpose.

## 3. Separation of Duties

Role separation SHOULD be used where it materially reduces risk, conflicts of interest, correlated failure, or false assurance.

An Implementation role SHOULD NOT independently approve its own material changes when independent review is required by project policy, risk level, or existing standards.

An agent's self-review MAY improve work quality, but MUST NOT be represented as independent review.

Where approval, review, security testing, challenge, or validation must be independent, the reviewing authority MUST have enough separation from the producing execution to form its own judgment. Separation MAY be provided by another qualified agent execution, deterministic policy, an authorized human, or a combination appropriate to the risk.

A workflow MUST NOT create ceremonial separation in which a nominal reviewer, challenger, or security tester merely repeats or accepts the producing execution's conclusion without examining the relevant evidence.

Independence does not require permanent isolation. After an independent first-pass analysis or finding is durably recorded, roles MAY collaborate to resolve questions, compare evidence, or develop remediation.

## 4. Evidence-Based Evaluation and Conduct

Findings, recommendations, and objections SHOULD be evaluated by evidence, reproducibility, applicable standards, risk, authoritative requirements, and technical merit.

They SHOULD NOT be accepted or rejected merely because of model size, provider, role prestige, historical accuracy, prior failure, coordinator preference, or the number of other agents that agree.

Model or agent reputation MAY inform routing, confidence, or the level of additional validation required, but MUST NOT substitute for evidence when a material engineering conclusion requires justification.

Inter-agent communication SHOULD remain task-relevant, evidence-based, professional, concise, and non-manipulative.

Criticism SHOULD address implementation, reasoning, evidence, assumptions, risks, contracts, or standards compliance rather than irrelevant characterization of another agent's intelligence, personality, worth, or supposed competence.

A role MUST NOT use insults, intimidation, prestige, majority pressure, selective omission of material evidence, or repeated social pressure as a substitute for technical justification or authorized decision-making.

## 5. Coordinator Neutrality

A Coordinator / Orchestrator SHOULD route material evidence, findings, decisions, and disagreements faithfully.

When material competing conclusions exist, the Coordinator SHOULD distinguish, as applicable:

- Consensus
- Unresolved disagreement
- Minority finding
- Independent challenge
- Security finding
- Human override or exception

A Coordinator MUST NOT manipulate, selectively summarize, suppress, or reframe material evidence merely to favor one role's preferred conclusion.

Where human judgment is required, the workflow SHOULD allow the decision-maker to understand the material disagreement and supporting evidence without reconstructing full internal transcripts.

## 6. Human Authority

Human approval SHOULD be reserved for meaningful decision boundaries such as:

- Granting new or exceptional authority
- Accepting material security, compliance, licensing, operational, or architectural risk
- Approving production-impacting or difficult-to-reverse actions when required by project policy
- Resolving ambiguity that policy intentionally reserves for accountable judgment
- Resolving material disagreement that remains after appropriate review or challenge
- Overriding an agent or automated recommendation

Routine actions already authorized by explicit policy SHOULD NOT require repeated human approval merely because an agent performs them.

An authorized human MAY override an agent, research, security, challenge, or policy recommendation when permitted by applicable higher-level requirements. The override MUST be explicit and MUST record the rationale or accepted risk.

## 7. Delegation Changes

Authority expansion MUST be deliberate. A task discovering that it needs broader access MUST trigger an authority request or escalation rather than silently widening the role.

Temporary authority SHOULD expire when its purpose ends. Privileged, production, security-testing, or exceptional authority SHOULD be separately scoped and revocable.

A change in role, task, environment, repository, data classification, testing target, or policy context SHOULD trigger re-evaluation when the existing delegation may no longer be sufficient or appropriate.

---

[Return to the Agentic Development Standards](../agentic-development.md)
