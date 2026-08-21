# Agentic Task Lifecycle and Escalation Standards

*Companion document in the Agentic Development Standards family*

This document defines task state, durable handoffs, bounded retries, escalation, approval, and human decision boundaries. It is authoritative for the detailed rules in its scope.

## 1. Task Definition and State

Agentic work MUST have a sufficiently explicit task boundary to determine completion, permitted scope, required validation, and escalation conditions.

A task SHOULD identify, where relevant:

- Objective and acceptance criteria
- Responsible role or execution
- Repository, workspace, environment, and data scope
- Applicable standards or project policy
- Required evidence and validation
- Authority limits
- Dependencies or predecessor decisions
- Conditions requiring review, approval, escalation, or termination

Material task state MUST be durable outside model context. An interrupted or replaced execution SHOULD be able to resume from authoritative task records without relying on hidden conversational memory.

## 2. Workflow Transitions and Handoffs

Meaningful workflow transitions SHOULD be represented by structured artifacts or records rather than uncontrolled free-form conversation alone.

A handoff SHOULD preserve enough information for the receiving role to understand:

- The task or question
- Work completed
- Evidence produced
- Known failures, risks, or uncertainty
- Decisions already made and their authority
- The next requested action

Implementations MAY define typed artifacts such as `TaskRequest`, `ReviewResult`, `ResearchResult`, `ToolRequest`, `ApprovalRequest`, `Escalation`, or `ValidationResult`. These names are illustrative; durable semantics matter more than the specific schema.

## 3. Routine Resolution and Human Boundaries

Agents SHOULD resolve routine problems within delegated authority without requiring a human to relay messages between roles.

A human SHOULD be involved when accountable judgment, new authority, exception acceptance, material risk acceptance, or another reserved decision is actually required.

Workflow design SHOULD distinguish notification from approval. Keeping a human informed MUST NOT be treated as equivalent to obtaining required authorization.

## 4. Escalation

An agent MUST escalate rather than circumvent policy when completion requires unavailable authority or an explicitly reserved decision.

An escalation SHOULD contain:

- What is blocked
- Why the current role cannot resolve it autonomously
- Relevant evidence and uncertainty
- Available options and consequences
- A recommendation when appropriate
- The exact approval, authority, information, or decision requested

Escalations SHOULD be concise enough to support efficient decisions without omitting material risk or evidence.

If an authorized decision rejects the requested action, the agent MUST follow the rejection, revise the approach within existing authority, or terminate the affected work. It MUST NOT repeatedly reframe the same request merely to obtain a different answer unless materially new evidence exists.

## 5. Bounded Retry and Recovery

Autonomous retry, repair, and correction loops MUST be bounded.

Bounds MAY be defined by attempt count, elapsed time, cost, resource consumption, changed scope, repeated failure signature, or another enforceable condition appropriate to the task.

Repeated failures SHOULD preserve diagnostic evidence and avoid destructive repetition. When the bound is reached, the workflow MUST enter a defined failure, escalation, or safe-termination state.

A retry MUST NOT silently weaken tests, security controls, validation criteria, or acceptance requirements to manufacture success.

## 6. Approval and Exception Records

Required approvals MUST be attributable to an authorized decision-maker and associated with the affected task, action, or exception.

Approval scope SHOULD be explicit enough to prevent an approval for one action from being reused as blanket authority for unrelated actions.

Exceptions and overrides MUST record the applicable rule or policy, decision-maker, rationale or accepted risk, scope, and expiration or review condition when temporary.

---

[Return to the Agentic Development Standards](../agentic-development.md)
