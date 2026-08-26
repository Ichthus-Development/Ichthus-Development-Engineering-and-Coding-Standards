# Agentic Audit, Identity, and Traceability Standards

*Companion document in the Agentic Development Standards family*

This document defines execution identity, attributable material actions, policy context, durable findings and dissent, and durable traceability for agentic engineering work. It is authoritative for the detailed rules in its scope.

## 1. Actor Identity

Material agentic actions SHOULD be attributable to a specific execution operating under a defined role and policy context.

Records that merely state that “AI” changed, approved, tested, challenged, or researched something are insufficient when the action is material enough to require attribution.

Attribution SHOULD distinguish, where relevant:

- The agent or execution identity
- Logical role
- Task or work item
- Workspace or environment
- Repository and relevant revision
- Governing policy or standards context
- Human approval or escalation references

Provider, model, and model version SHOULD be recorded when they are available and materially relevant to reproducibility, governance, incident analysis, contractual obligations, correlation analysis, or evaluation. Their absence MUST NOT make the rest of the execution unattributable when other stable identifiers are available.

## 2. Execution and Correlation

Persistent or orchestrated workflows SHOULD assign durable identifiers sufficient to correlate related task, run, workspace, review, research, security finding, challenge, approval, and validation records.

An implementation MAY use fields such as agent identifier, role, run identifier, task identifier, workspace identifier, repository revision, policy version, finding identifier, challenge identifier, or approval reference. This standard does not require a particular schema in its initial version.

Identifiers MUST have documented semantics when ambiguity could cause incorrect attribution or policy decisions.

Where independence is material, records SHOULD preserve enough execution metadata to determine whether purportedly independent analyses shared relevant model, provider, prompt framing, evidence ordering, source context, or prior conclusions when that information is available and operationally useful.

## 3. Material Actions, Findings, and Decisions

Material actions and decisions MUST be traceable at a level proportionate to their impact.

Traceability SHOULD preserve, when applicable:

- What action, review, challenge, or test was requested and performed
- Who or what performed it
- Which role and authority applied
- Relevant inputs or evidence without unnecessarily retaining sensitive content
- Validation results
- Security findings and retest disposition
- Independent challenge disposition
- Material minority findings or unresolved dissent
- Review disposition
- Escalations, approvals, denials, accepted risks, or overrides
- Repository or environment outcome
- Time and ordering information sufficient to reconstruct material workflow state

A material finding SHOULD NOT disappear from the durable record merely because subsequent agents, a majority of agents, or the original implementation disagree with it. The record SHOULD preserve its disposition, evidence, and authority for closure, rejection, acceptance, or supersession.

Auditability MUST NOT become an excuse to collect full prompts, secrets, sensitive payloads, private reasoning, or unlimited transcripts when structured metadata and durable outcomes can satisfy the traceability requirement.

## 4. Durable Project Record

Model context MUST NOT be treated as the authoritative project record.

Material requirements, decisions, approvals, research findings, security findings, challenge results, review results, validation results, minority findings, and unresolved risks SHOULD be stored in durable project systems or artifacts appropriate to their purpose.

An execution SHOULD be able to derive the authoritative current state necessary for its assigned responsibility from durable project records and resolvable references without requiring a prior execution's complete conversation.

Agent-to-agent workflow records SHOULD preserve durable outcomes, evidence, findings, and decisions rather than conversational history when those outcomes are sufficient to continue the work correctly.

A durable record SHOULD remain understandable without requiring access to the full conversational transcript that produced it.

When a decision or finding disposition changes, the project record SHOULD preserve enough history to identify the superseded conclusion and the authority or evidence supporting the change.

Detailed execution records MAY contain more information than normal human-facing completion or escalation summaries. Reporting SHOULD reference authoritative records rather than duplicate them when reliable retrieval is available.

## 5. Disagreement and Disposition Traceability

Where a material decision includes competing conclusions, the durable record SHOULD distinguish the prevailing recommendation from independent challenge, security findings, minority findings, and human overrides when applicable.

Consensus counts or vote-like summaries MAY be recorded for workflow information, but MUST NOT replace the evidence and disposition required for material findings.

A challenge result that upholds the prevailing conclusion SHOULD be preserved as a valid completed outcome rather than represented as a failed attempt to find disagreement.

A dissenting finding MAY be closed when evidence, authorized decision, superseding requirements, or successful remediation resolves it. Closure SHOULD record the basis rather than relying on disappearance from subsequent summaries.

## 6. Policy and Governance Context

Where agent behavior depends on versioned policy, governance rules, approval catalogs, capability profiles, or orchestration configuration, material execution records SHOULD identify the applicable version or revision when practical.

Policy changes MUST NOT retroactively imply that an earlier action was authorized under rules that did not apply when the action occurred.

Human overrides, exceptions, and accepted risks MUST be attributable and linked to the scope they govern.

---

[Return to the Agentic Development Standards](../agentic-development.md)
