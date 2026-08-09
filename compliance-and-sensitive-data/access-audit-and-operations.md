# Sensitive-Data Access, Audit, and Operations Standards

*Companion document in the Compliance and Sensitive Data Standards family*

This document defines operational safeguards for diagnostics, authorization, auditing, and incident awareness. It is authoritative for the detailed rules in its scope.

## 1. Logging, Diagnostics, Error Messages, and Telemetry

Sensitive data MUST NOT be written to logs, diagnostics, telemetry, screenshots, console output, temporary files, or exception messages unless explicitly required, approved, access-controlled, and documented.

Diagnostics SHOULD preserve troubleshooting value without exposing sensitive values. Prefer stable identifiers, classifications, field names, lengths, counts, hashes specifically approved for correlation, and structured error codes over raw content.

Diagnostics represent facts; their design MUST make clear whether a value was omitted, redacted, masked, unavailable, invalid, or unauthorized. Silent removal that changes the meaning of a diagnostic is discouraged.

Logging frameworks, exception serializers, request tracing, object inspection, application-performance monitoring, and support-bundle generation MUST be reviewed for automatic capture of sensitive fields.

Production logging levels MUST NOT be changed in a way that exposes sensitive values without explicit approval and a documented rollback and disposal plan.

Systems SHOULD provide enough non-sensitive diagnostic context to investigate failures, authorization decisions, and integration outcomes without requiring disclosure of protected content.

## 2. Access Control and Authorization

Access to sensitive data MUST be explicitly authorized and limited to the minimum necessary identities, roles, processes, fields, records, and operations.

Authentication establishes identity; authorization determines permitted action. Systems MUST NOT treat successful authentication as unrestricted authorization.

Authorization MUST be enforced by trusted system boundaries and MUST NOT rely solely on hidden UI elements, client-side checks, naming conventions, or undocumented operator behavior.

Privileged access, service accounts, emergency access, impersonation, support access, and bulk export capabilities MUST be intentionally designed, auditable, and revocable.

Access decisions SHOULD deny by default when required identity, policy, classification, or context is missing or invalid.

Projects SHOULD periodically review access paths and remove obsolete permissions, accounts, tokens, integrations, and data copies.

### 2.1 Tenant, Client, Group, and Record-Level Isolation

Tenant, client, employer, group, plan, school, patient, member, dependent, employee, account, and record boundaries are authorization boundaries when they limit who may access sensitive information.

User-supplied identifiers, URL values, hidden fields, client-side state, filenames, or object names MUST NOT be treated as proof that the caller is authorized to access the referenced data.

Authorization SHOULD be evaluated against trusted identity and server-side policy for each sensitive operation. Queries, caches, indexes, exports, background jobs, reports, and integrations MUST preserve the same isolation boundaries as interactive application access.

Cross-tenant or cross-client access MUST be explicit, justified, narrowly scoped, and auditable. Systems MUST fail closed when tenant, ownership, group, or record-level context is missing, conflicting, or invalid.

### 2.2 Privileged, Support, Impersonation, and Emergency Access

Administrative, support, impersonation, and emergency or break-glass access MUST be explicitly designed rather than implemented as an undocumented bypass.

Such access SHOULD require:

- A specific authorized identity rather than a shared account
- A documented reason or incident reference
- The minimum necessary scope and duration
- Strong authentication appropriate to the risk
- Audit records of activation, actions, and termination
- Notification or retrospective review where required
- Automatic expiration or prompt revocation when the purpose ends

Impersonation MUST clearly distinguish the support or administrative actor from the represented user. Audit records MUST NOT falsely attribute privileged actions solely to the represented user.

Emergency access MUST NOT silently disable logging, data classification, export restrictions, or other safeguards unrelated to resolving the emergency.

### 2.3 Bulk Access and High-Impact Operations

Bulk viewing, search, export, import, correction, migration, deletion, reclassification, and permission changes create a larger potential impact than equivalent single-record operations and MUST receive controls proportionate to that impact.

Bulk operations SHOULD include:

- Explicit authorization separate from ordinary record access
- Bounded filters, counts, and scope confirmation before execution
- Safe previews that do not unnecessarily reveal full sensitive values
- Idempotent or restartable behavior where practical
- Reconciliation of attempted, successful, rejected, and partial results
- Protection against accidental cross-tenant or cross-client scope
- Auditability without copying full sensitive payloads into audit records
- Controlled output location, retention, and disposal

Destructive or difficult-to-reverse bulk actions SHOULD require additional confirmation, approval, staged execution, or recoverability appropriate to the risk.

Partial failure MUST be reported explicitly. A bulk operation MUST NOT claim complete success when records were skipped, rejected, duplicated, partially transformed, or left in an indeterminate state.

## 3. Auditability and Traceability

Systems handling sensitive or audit-sensitive records MUST provide traceability appropriate to the applicable obligations and risk.

Audit records SHOULD identify, when appropriate:

- The actor or system identity
- The action attempted or completed
- The affected record or resource using a safe identifier
- The time and relevant environment
- The authorization or policy outcome
- The source or integration involved
- The success, failure, or disposition

Audit records MUST NOT disclose sensitive content unnecessarily. Auditability and confidentiality are simultaneous requirements.

Audit events MUST be sufficiently protected from unauthorized alteration, deletion, or repudiation. Time sources, identity propagation, correlation identifiers, and event semantics SHOULD be consistent and documented.

Sensitive data handling decisions SHOULD be documented close to the implementation. External standards, contractual rules, and business obligations MUST be traceable to their source, version, or responsible authority where practical.

## 4. Incident Awareness

Developers and operators MUST know how to report suspected exposure, unauthorized access, accidental disclosure, secret leakage, data loss, integrity failure, or prohibited use of sensitive information.

Systems SHOULD make security-relevant failures observable without exposing protected values. Hidden failure, silent fallback, and automatic weakening of controls are prohibited.

When an incident is suspected:

- Preserve relevant evidence without unnecessarily copying sensitive data
- Stop further disclosure when safe and authorized to do so
- Notify the designated incident, security, privacy, legal, compliance, or business authority
- Avoid unilateral destruction or alteration of records that may be required for investigation, notification, audit, or legal hold

This document does not define breach determination or notification obligations. Those determinations belong to authorized organizational and legal processes.

---

[Return to the Compliance and Sensitive Data Standards](../compliance-and-sensitive-data.md)
