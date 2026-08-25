# Agentic Task Lifecycle and Escalation Standards

*Companion document in the Agentic Development Standards family*

This document defines task state, context assembly, durable handoffs, bounded retries, escalation, approval, completion reporting, and human decision boundaries. It is authoritative for the detailed rules in its scope.

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

Human requirements MAY begin as verbose, conversational, exploratory, or incomplete input. A planning, coordination, or equivalent stage MAY normalize that input into a durable task artifact before downstream execution. Humans SHOULD NOT be required to communicate in machine-oriented schemas merely because internal workflow components benefit from structured state.

## 2. Minimum-Sufficient Context and Context Assembly

An agent execution SHOULD receive the smallest authoritative context reasonably sufficient to perform its assigned responsibility correctly.

Minimum-sufficient context is not minimum token count. Context assembly SHOULD preserve information materially necessary to understand, where relevant:

- The assigned task and acceptance criteria
- Applicable standards, policies, and authority limits
- Relevant architecture decisions, contracts, schemas, or external requirements
- Relevant source artifacts, revisions, changes, or repository state
- Prior authoritative decisions affecting the work
- Known risks, failures, uncertainty, and unresolved concerns
- Required validation
- The requested output, disposition, or decision

Unrelated conversational history SHOULD NOT be included merely because it is available.

Implementations SHOULD NOT routinely provide complete project conversations, transcripts, repositories, research histories, or policy collections to every execution when targeted retrieval, changed artifacts, or stable references can provide sufficient context.

Over-compression that causes material ambiguity, repeated rediscovery, avoidable failed attempts, contract violations, or incorrect work SHOULD be treated as failed optimization rather than successful resource reduction.

A context-building mechanism MAY be an orchestrator, retrieval system, deterministic service, agent, human, or another component appropriate to the workflow. The mechanism SHOULD select context according to the receiving responsibility rather than accumulate information indiscriminately.

Where authoritative durable material already exists, context and handoffs SHOULD prefer stable references to unnecessary duplication when the receiving execution can resolve those references reliably. References MAY identify standards, policy versions, architecture decisions, task records, API or schema contracts, repository revisions, validation results, research artifacts, or approval records.

References MUST NOT become opaque shorthand that prevents the receiving execution from obtaining information necessary to perform the task correctly.

## 3. Workflow Transitions and Handoffs

Meaningful workflow transitions SHOULD be represented by structured artifacts or records rather than uncontrolled free-form conversation alone.

Machine-to-machine handoffs SHOULD favor task-specific structured semantics over conversational prose when practical. JSON, YAML, typed messages, APIs, queues, database records, or other representations MAY be used; this standard does not prescribe a serialization format.

A handoff SHOULD preserve enough information for the receiving role to understand:

- The task or question
- The authoritative artifact, revision, or state being acted upon
- Work completed or current disposition
- Evidence produced
- Applicable standards, policy, or authority references when material
- Known failures, risks, or uncertainty
- Decisions already made and their authority
- The next requested action or required disposition

Machine-facing handoffs generally SHOULD omit greetings, conversational transitions, stylistic filler, repeated background explanation, and redundant copies of reliably retrievable authoritative material.

Semantic completeness MUST NOT be sacrificed for brevity. A structurally compact handoff that omits material requirements or makes its meaning ambiguous is defective regardless of token count.

Implementations MAY define typed artifacts such as `TaskRequest`, `ReviewResult`, `ResearchResult`, `ToolRequest`, `ApprovalRequest`, `Escalation`, or `ValidationResult`. These names are illustrative; durable semantics matter more than the specific schema.

Agent-to-agent communication SHOULD pass durable outcomes and evidence rather than conversational history wherever practical.

## 4. Consumer-Oriented Communication

Workflow output SHOULD be designed for the responsibility and needs of its consumer.

Agent-to-agent communication SHOULD favor:

- Structured state
- Stable references
- Concise semantics
- Explicit requested action or disposition
- Machine-parseable fields when they materially improve reliability

Agent-to-human communication SHOULD favor:

- The decision or action that matters to the human
- Concise explanation
- Material evidence and uncertainty
- Risk and consequences
- Recommendation when appropriate
- The exact decision, approval, information, or authority requested

A human SHOULD NOT be required to reconstruct lengthy internal agent conversations merely to determine why intervention is required.

Human-facing summaries MAY omit intermediate workflow detail that is not relevant to the decision while preserving links or references to authoritative evidence and detailed records when needed.

System complexity SHOULD be absorbed by the workflow layer best able to manage it rather than pushed outward to each agent or human consumer. An orchestrated workflow MAY perform substantial internal routing, retrieval, research, validation, and review while presenting a human with one concise actionable decision package.

## 5. Routine Resolution and Human Boundaries

Agents SHOULD resolve routine problems within delegated authority without requiring a human to relay messages between roles.

A human SHOULD be involved when accountable judgment, new authority, exception acceptance, material risk acceptance, or another reserved decision is actually required.

Workflow design SHOULD distinguish notification from approval. Keeping a human informed MUST NOT be treated as equivalent to obtaining required authorization.

Human attention is a constrained workflow resource. Agentic systems SHOULD reduce unnecessary interruption, status-chasing, and routine supervision while preserving human authority at meaningful decision boundaries.

A safe workflow SHOULD NOT require a human to continuously observe routine agent activity merely to detect whether policy is being followed. Material exceptions, failures, and reserved decisions SHOULD be surfaced explicitly.

## 6. Escalation

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

## 7. Bounded Retry and Recovery

Autonomous retry, repair, and correction loops MUST be bounded.

Bounds MAY be defined by attempt count, elapsed time, cost, resource consumption, changed scope, repeated failure signature, or another enforceable condition appropriate to the task.

Repeated failures SHOULD preserve diagnostic evidence and avoid destructive repetition. When the bound is reached, the workflow MUST enter a defined failure, escalation, or safe-termination state.

A retry MUST NOT silently weaken tests, security controls, validation criteria, or acceptance requirements to manufacture success.

Repeated rediscovery of authoritative information that could be retained or retrieved through durable task state SHOULD be treated as workflow inefficiency and corrected when material.

## 8. Completion and Reporting

A completion or result artifact SHOULD make it possible for its consumer to determine quickly:

- What was requested
- What changed, was produced, or was decided
- Whether acceptance criteria were satisfied
- Which deterministic checks actually ran and their results
- Which relevant checks failed, were unavailable, or were skipped
- Material unresolved risks, uncertainty, or follow-up work
- Whether further human action is required
- Where authoritative artifacts, revisions, evidence, or records can be found

Completion reporting MUST distinguish actual validation from inference or expectation.

Execution information and reporting information need not be identical. Detailed diagnostics, logs, and trace records MAY remain available separately when they are useful for debugging, audit, or investigation. The normal completion result SHOULD optimize for fast comprehension without concealing material information.

Agents SHOULD NOT reproduce every intermediate step, prompt, discussion, or reasoning trace merely because it exists.

## 9. Approval and Exception Records

Required approvals MUST be attributable to an authorized decision-maker and associated with the affected task, action, or exception.

Approval scope SHOULD be explicit enough to prevent an approval for one action from being reused as blanket authority for unrelated actions.

Exceptions and overrides MUST record the applicable rule or policy, decision-maker, rationale or accepted risk, scope, and expiration or review condition when temporary.

---

[Return to the Agentic Development Standards](../agentic-development.md)
