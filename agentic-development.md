# Agentic Development Standards

*Engineering Governance for Delegated AI and Agentic Workflows*

## 1. Purpose and Scope

This document defines baseline engineering standards for software-development work performed in whole or in part by AI or other agentic workers operating under delegated authority.

These standards apply across implementation maturity, including:

- A human developer directing a single coding agent
- Multiple specialized agents operating under direct human supervision
- Orchestrated workflows containing planning, implementation, research, review, testing, provisioning, or other logical roles
- Persistent autonomous or semi-autonomous development workflows operating under policy and human escalation

An **agentic worker** is an engineering actor operating under delegated authority. The term describes responsibility and authority, not a particular model, provider, product, process topology, or implementation technology.

Agent-produced work remains subject to the same engineering, security, compliance, accessibility, language, database, UI, dependency, and quality standards as human-produced work. This document family governs how agentic work is authorized, performed, reviewed, escalated, and traced; it does not create a separate definition of acceptable software quality.

## 2. Foundational Principles

The following requirements apply across this document family:

- Agentic workers MUST operate within explicitly delegated authority.
- Authority MUST NOT be inferred from technical capability, task urgency, model confidence, prior access, or an agent's own request.
- Least privilege MUST apply to repositories, tools, credentials, data, infrastructure, execution environments, and decision-making authority.
- An agent MUST NOT bypass, weaken, reinterpret, or silently work around a policy constraint merely to complete a task.
- When required authority is unavailable, the agent MUST stop the affected action and escalate through the defined workflow.
- Deterministic enforcement SHOULD be preferred over prompt-only instruction when a requirement can be enforced reliably by permissions, policy engines, branch protection, sandboxing, CI, static analysis, schemas, or other mechanical controls.
- Material actions, decisions, approvals, exceptions, and validation results MUST be traceable at a level proportionate to their impact.
- Model context MUST NOT be treated as the authoritative project record. Material state and decisions MUST survive context loss in durable project artifacts or systems of record.
- Agent executions SHOULD receive minimum-sufficient authoritative context for the responsibility being performed rather than accumulated conversational history merely because it is available.
- Model context and inference MUST be treated as engineering resource consumption subject to the repository's [Resource Efficiency](principles.md#resource-efficiency) standards.
- Optimization of tokens, context size, inference time, model cost, or workflow speed MUST NOT sacrifice correctness, security, maintainability, validation quality, usability, or information materially necessary to perform the assigned responsibility.
- Autonomous retry, correction, and recovery loops MUST be bounded by count, time, cost, scope, or another explicit limit appropriate to the workflow.
- Human overrides and exceptions MUST be explicit, attributable, and recorded with the accepted risk or rationale.
- Human intervention SHOULD occur at meaningful decision boundaries rather than serving as the routine message bus or routing mechanism for otherwise authorized work.

These requirements extend the repository-wide principles of explicit design, proportional resource use, consumer-oriented simplicity, conscious deviations, enforceability, and tooling alignment defined in [Engineering Principles](principles.md).

## 3. Terminology

For this document family:

- **Agentic worker / agent** — A software-development actor capable of reasoning, tool use, or task execution under delegated authority.
- **Role** — A logical responsibility with defined authority and constraints. A role does not imply a dedicated model or process.
- **Authority** — Permission to perform a class of actions within defined scope and conditions.
- **Delegation** — Explicit assignment of authority from an authorized person, policy, system, or workflow to an agentic role or execution.
- **Human authority / approver** — A person authorized to make a decision or grant an exception that the agentic workflow cannot grant to itself.
- **Material action** — An action whose effect, risk, cost, irreversibility, security impact, production impact, or governance significance warrants durable traceability or review.
- **Deterministic validation** — Validation performed by reproducible tooling such as compilers, tests, analyzers, linters, migration validators, or policy checks rather than by model assertion alone.
- **Execution** — A specific agent run or bounded activity operating under a defined role, task, workspace, and policy context.
- **Efficiency** — Achieving the needed result while avoiding unnecessary consumption of context, inference, compute, network, storage, human attention, or other resources.
- **Expediency** — Reducing unnecessary delay between a need, result, handoff, decision, or response.
- **Effectiveness** — Producing a correct, useful, maintainable, safe, and fit-for-purpose engineering result.
- **Minimum-sufficient context** — The smallest authoritative context reasonably sufficient for an execution to perform its assigned responsibility correctly without material ambiguity or avoidable rediscovery.

Implementations MAY use different names when their meaning and authority boundaries remain equivalent.

## 4. Authority and Delegation

Delegated authority MUST define enough scope to determine what the agent may and may not do without additional approval.

Authority SHOULD identify, where relevant:

- Permitted repositories, branches, workspaces, environments, and systems
- Permitted read, write, execute, network, deployment, and administrative operations
- Permitted data classifications and credential scopes
- Allowed dependency, tooling, and provisioning actions
- Review or approval requirements
- Time, cost, retry, resource, or execution limits
- Conditions that require escalation

Possession of credentials, filesystem access, administrator capability, network reachability, or an available tool MUST NOT be treated as authorization to use that capability for every technically possible action.

An agent MUST NOT grant itself additional authority. A coordinator or orchestrator MAY route work and apply previously approved policy, but MUST NOT silently convert missing authority into granted authority.

Previously approved policy MAY delegate repeatable decisions to automated enforcement or an approved catalog. This is preferred when it prevents routine human approval from becoming a bottleneck without expanding agent authority implicitly.

See [Roles and Authority](agentic-development/roles-and-authority.md) for detailed role separation and delegation requirements.

## 5. Workflow and Persistent State

Agentic workflows MUST preserve material task state outside transient model context.

Meaningful handoffs and workflow transitions SHOULD use structured, durable artifacts or records. Examples include task requests, review results, research results, tool requests, approval requests, escalations, and validation results. Specific names and schemas are implementation-dependent.

A durable handoff SHOULD identify the task or decision, relevant evidence, current state, responsible role, and next permitted action without requiring reconstruction of an entire chat transcript.

Agents SHOULD resolve routine issues within delegated authority. When escalation is required, the escalation SHOULD present a concise decision package containing:

- What is blocked
- Why autonomous resolution is unavailable, prohibited, or inadvisable
- Relevant evidence and material uncertainty
- Available options
- The agent's recommendation when appropriate
- The exact decision or authority required

Repeated failure MUST NOT continue indefinitely. Retry and correction limits MUST eventually produce a defined failure state, escalation, or safe termination.

See [Task Lifecycle and Escalation](agentic-development/task-lifecycle-and-escalation.md).

## 6. Resource, Context, and Outcome Priorities

Efficiency, expediency, and effectiveness SHOULD be balanced according to the responsibility being performed. None SHOULD be optimized in isolation.

Machine-to-machine handoffs often benefit from efficiency through concise semantics, structured state, and stable references. Engineering execution generally prioritizes effectiveness because a fast or inexpensive incorrect result does not satisfy the engineering objective. Human-facing results and escalations often benefit from expediency because the consumer should be able to identify the material outcome or requested decision quickly.

These are design tendencies rather than fixed ordering rules. A shorter handoff that omits a necessary contract is not efficient overall; a faster implementation that creates fragility is not expedient in any meaningful project sense; and an exhaustive report that obscures the decision in transcript-level detail may reduce effectiveness for its consumer.

Agentic workflows SHOULD optimize for proportional total resource expenditure required to reach a correct outcome rather than minimum input tokens, minimum model cost, or minimum elapsed time in isolation.

Model usage consumes resources regardless of deployment model. Depending on implementation, relevant costs MAY include:

- Input context and output volume
- Inference duration and hosted usage cost
- CPU, GPU, memory, or VRAM utilization
- Electrical power and thermal load
- Network use
- Throughput and concurrency capacity
- Human review, interruption, and decision attention

Measurement and telemetry SHOULD be proportionate to operational value. This standard does not require exhaustive per-execution accounting when the information would not materially improve engineering or operational decisions.

See [Task Lifecycle and Escalation](agentic-development/task-lifecycle-and-escalation.md) for minimum-sufficient context, handoffs, and consumer-oriented communication.

## 7. Deterministic Enforcement and Agent Judgment

Agent reasoning MAY design, interpret, prioritize, explain, and investigate work, but it MUST NOT substitute a textual claim for deterministic validation that is available and required.

Builds, compiler diagnostics, automated tests, static analysis, linters, schema validation, migration validation, policy checks, and equivalent deterministic controls SHOULD be executed by their authoritative tooling when available.

Prompt instructions alone SHOULD NOT be treated as sufficient enforcement for permissions, protected branches, secret access, production access, dependency restrictions, or other controls that can be enforced mechanically without disproportionate cost or complexity.

Mechanical enforcement does not eliminate engineering judgment. When deterministic tooling cannot determine correctness, an authorized reviewer or decision-maker remains responsible for the judgment appropriate to the risk.

See [Review and Validation](agentic-development/review-and-validation.md).

## 8. Relationship to Existing Standards

This family applies alongside the rest of the Ichthus Development standards:

- [Engineering Principles](principles.md) remains authoritative for repository-wide philosophy, rule terminology, resource efficiency, conscious deviations, and enforcement.
- [Approved Libraries and Dependencies](approved-libraries.md) remains authoritative for dependency evaluation and approval criteria. This family defines agent behavior when a tool or dependency is unavailable or unapproved.
- [Compliance and Sensitive Data Standards](compliance-and-sensitive-data.md) remains authoritative for sensitive-data classification and handling. This family defines agent-specific access, authority, and exposure boundaries.
- Language, database, UI, accessibility, formatting, and data-format standards remain fully applicable to agent-generated work.

A project MUST NOT use agentic implementation as justification to weaken an existing engineering or compliance requirement.

## 9. Document Family

This standard is organized as a document family. This root document defines shared scope, principles, terminology, authority concepts, and navigation. Each companion document owns the detailed rules for a distinct responsibility:

- [Roles and Authority](agentic-development/roles-and-authority.md) — logical roles, delegated authority, separation of duties, and human authority boundaries.
- [Task Lifecycle and Escalation](agentic-development/task-lifecycle-and-escalation.md) — task state, context assembly, handoffs, bounded retries, escalation, approval, completion reporting, and human decision boundaries.
- [Repository and Workspace Standards](agentic-development/repository-and-workspace.md) — isolated work, concurrency, repository history, branches, worktrees, and protected change paths.
- [Tools, Dependencies, and Research](agentic-development/tools-dependencies-and-research.md) — tool requests, dependency discovery, research evidence, approval routing, catalogs, and provisioning boundaries.
- [Review and Validation](agentic-development/review-and-validation.md) — independent review, deterministic verification, test evidence, and truthful validation reporting.
- [Agent Security and Secrets](agentic-development/security-and-secrets.md) — least-privilege agent access, credential exposure, environment boundaries, untrusted external content, and privilege escalation.
- [Audit, Identity, and Traceability](agentic-development/audit-identity-and-traceability.md) — execution identity, attributable material actions, policy context, durable records, and audit semantics.

Companion documents use local section numbering. Their numbers describe structure within that document and do not represent sections of a reconstructed monolithic standard.

## 10. Non-Goals

This family does not attempt to:

- Require a particular AI provider, model, agent framework, or orchestration platform
- Require every logical role to be implemented by a separate model or agent instance
- Replace project management, source-control, CI/CD, security, dependency, compliance, or coding standards owned elsewhere
- Require human approval for routine actions already permitted by explicit delegated policy
- Require humans to communicate through machine-oriented schemas
- Require retention of full prompts, private reasoning, or complete agent conversations merely for auditability
- Treat agent output as inherently correct, incorrect, malicious, or trustworthy
- Define a complete autonomous-development organization in this first version

Future refinements MAY define reusable policy schemas, structured workflow contracts, risk tiers, approved agent capability profiles, or reference implementations when practical experience justifies standardization.

---

*Ichthus Development Engineering and Coding Standards exist to serve understanding, not fashion.*

© Gold Fish Bowl, LLC, DBA Ichthus Development
