# Agentic Audit, Identity, and Traceability Standards

*Companion document in the Agentic Development Standards family*

This document defines execution identity, attributable material actions, policy context, and durable traceability for agentic engineering work. It is authoritative for the detailed rules in its scope.

## 1. Actor Identity

Material agentic actions SHOULD be attributable to a specific execution operating under a defined role and policy context.

Records that merely state that “AI” changed, approved, tested, or researched something are insufficient when the action is material enough to require attribution.

Attribution SHOULD distinguish, where relevant:

- The agent or execution identity
- Logical role
- Task or work item
- Workspace or environment
- Repository and relevant revision
- Governing policy or standards context
- Human approval or escalation references

Provider, model, and model version SHOULD be recorded when they are available and materially relevant to reproducibility, governance, incident analysis, contractual obligations, or evaluation. Their absence MUST NOT make the rest of the execution unattributable when other stable identifiers are available.

## 2. Execution and Correlation

Persistent or orchestrated workflows SHOULD assign durable identifiers sufficient to correlate related task, run, workspace, review, research, approval, and validation records.

An implementation MAY use fields such as agent identifier, role, run identifier, task identifier, workspace identifier, repository revision, policy version, or approval reference. This standard does not require a particular schema in its initial version.

Identifiers MUST have documented semantics when ambiguity could cause incorrect attribution or policy decisions.

## 3. Material Actions and Decisions

Material actions and decisions MUST be traceable at a level proportionate to their impact.

Traceability SHOULD preserve, when applicable:

- What action was requested and performed
- Who or what performed it
- Which role and authority applied
- Relevant inputs or evidence without unnecessarily retaining sensitive content
- Validation results
- Review disposition
- Escalations, approvals, denials, or overrides
- Repository or environment outcome
- Time and ordering information sufficient to reconstruct material workflow state

Auditability MUST NOT become an excuse to collect full prompts, secrets, sensitive payloads, or unlimited transcripts when structured metadata can satisfy the traceability requirement.

## 4. Durable Project Record

Model context MUST NOT be treated as the authoritative project record.

Material requirements, decisions, approvals, research findings, review results, validation results, and unresolved risks SHOULD be stored in durable project systems or artifacts appropriate to their purpose.

A durable record SHOULD remain understandable without requiring access to the full conversational transcript that produced it.

When a decision changes, the project record SHOULD preserve enough history to identify the superseded decision and the authority for the change.

## 5. Policy and Governance Context

Where agent behavior depends on versioned policy, governance rules, approval catalogs, capability profiles, or orchestration configuration, material execution records SHOULD identify the applicable version or revision when practical.

Policy changes MUST NOT retroactively imply that an earlier action was authorized under rules that did not apply when the action occurred.

Human overrides, exceptions, and accepted risks MUST be attributable and linked to the scope they govern.

---

[Return to the Agentic Development Standards](../agentic-development.md)
