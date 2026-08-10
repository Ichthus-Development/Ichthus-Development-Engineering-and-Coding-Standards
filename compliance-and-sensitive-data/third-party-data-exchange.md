# Third-Party Data Exchange Standards

*Companion document in the Compliance and Sensitive Data Standards family*

This document defines standards for transmitting sensitive data and exchanging it with clients, vendors, carriers, PBMs, banks, schools, government systems, and other external parties. It is authoritative for the detailed rules in its scope.

## 1. Transmission and Integration

Sensitive data MUST be transmitted only through approved, authenticated, and appropriately protected channels.

Transport security MUST fail closed when confidentiality or integrity cannot be established. Certificate-validation failures, hostname mismatches, expired trust material, or unsupported security requirements MUST NOT be silently ignored.

Integrations MUST define:

- The data exchanged
- The authorized sender and recipient
- The purpose and permitted use
- Authentication and authorization requirements
- Transport and message-protection requirements
- Error, retry, replay, and duplicate-handling behavior
- Retention and disposal responsibilities
- Audit and reconciliation expectations

Sensitive data MUST NOT be placed in URLs or query strings when those values may be retained by browsers, proxies, servers, analytics tools, or logs.

Inbound data MUST be treated according to its content and obligations, not according to trust in the sender. External files and messages MUST be validated before use, and malformed input MUST fail safely without exposing its sensitive contents.

### 1.1 Third-Party Exchanges, Processors, and Downstream Recipients

Before sensitive data is received from or disclosed to a third party, the project MUST identify:

- The legal and business identities and roles of the parties
- The authority, agreement, and documented purpose for the exchange
- The data owner, system of record, and responsible decision-makers
- Every required data element and its classification
- The direction, frequency, volume, format, protocol, and environment of the exchange
- Authentication, authorization, transport, message-integrity, and key-management requirements
- Service providers, subprocessors, subcontractors, intermediaries, and downstream recipients
- Permitted uses, prohibited uses, and redisclosure restrictions
- Validation, acknowledgement, rejection, correction, retry, replay, duplicate, and reconciliation behavior
- Logging, audit, incident-notification, retention, return, destruction, and termination responsibilities
- Test, certification, onboarding, support, and production-data-access requirements

Authorization to receive data from a third party does not automatically authorize every internal use, copy, display, export, or downstream disclosure. Likewise, a third party's request for data does not establish authority to provide it.

Third-party platforms, portals, managed file-transfer services, clearinghouses, cloud services, carriers, PBMs, banks, schools, government systems, consultants, and support providers MUST be included in the sensitive-data boundary when they create, receive, maintain, transmit, or can access sensitive information.

The project MUST identify whether an applicable BAA, IMA, DUA, DSA, ISA, NDA, security addendum, service agreement, or other contract permits or requires the exchange. Contractual labels MUST NOT substitute for review of the executed terms.

Changes to a third party, subprocessor, endpoint, hosting region, transport, schema, purpose, or downstream use MUST trigger review before the changed flow handles sensitive data.

### 1.2 Completeness, Accuracy, and Data-Minimization Boundaries

Data minimization does not authorize a project to omit, truncate, mask, alter, or de-identify information when an applicable requirement or authorized data contract requires complete and accurate data.

When complete or detailed sensitive information is required for an authorized exchange, the project MUST document:

- Why each sensitive element is necessary
- Which source is authoritative
- Which transformations are permitted
- How completeness and accuracy are validated
- How omissions, conflicts, rejections, and corrections are resolved
- Which systems and parties receive the complete value
- How the expanded sensitive-data scope is protected and audited

Transformation logic MUST preserve required meaning, precision, relationships, identifiers, code systems, units, signs, dates, and record boundaries. Silent normalization, coercion, truncation, defaulting, or substitution that changes business or regulatory meaning is prohibited.

Received data MUST NOT be presumed complete, accurate, current, non-duplicated, or authorized merely because it arrived through an authenticated channel. Validation and reconciliation SHOULD preserve source fidelity while reporting discrepancies without exposing sensitive values unnecessarily.

Rejected records, acknowledgements, reconciliation reports, error files, retransmissions, and correction feeds may contain the same or greater sensitivity as the primary exchange and MUST receive equivalent review and protection.

If a third-party requirement materially expands the project's data scope, architecture, access model, retention, auditability, testing, operational support, cost, or risk, that expansion MUST be documented and approved before implementation or production data access.

---

[Return to the Compliance and Sensitive Data Standards](../compliance-and-sensitive-data.md)

