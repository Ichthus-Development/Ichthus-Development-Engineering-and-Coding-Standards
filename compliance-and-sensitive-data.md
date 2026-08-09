# Compliance and Sensitive Data Standards

*Baseline Engineering Expectations for Protected, Regulated, Confidential, and Sensitive Information*

## 1. Purpose and Scope

This document defines baseline engineering expectations for systems that collect, receive, generate, process, transform, store, transmit, display, export, log, archive, or dispose of sensitive information.

Sensitive information includes, but is not limited to:

- Protected health information (PHI)
- Personally identifiable information (PII)
- Confidential business and client information
- Credentials, secrets, tokens, certificates, and encryption keys
- Financial, payroll, benefit, claim, student, customer, employee, patient, member, and dependent information
- Payment card data
- Audit-sensitive and legally significant records
- Regulated data
- Copyrighted and licensed materials
- Information restricted by contract, policy, or business obligation

These standards apply to application code, libraries, databases, APIs, integrations, imports, exports, scripts, reports, user interfaces, logs, diagnostics, telemetry, test assets, support tools, operational procedures, and development workflows.

Sensitive data MUST be treated as a liability unless a documented business, legal, operational, or contractual requirement justifies its collection, storage, transmission, display, logging, or retention.

## 2. Non-Legal and Non-Certification Disclaimer

This document provides engineering standards, not legal advice. It does not interpret law, determine whether a law or regulation applies, replace qualified legal or compliance review, or certify that a project or organization is compliant.

Following these standards does not, by itself, make a project compliant with HIPAA, HITECH, PHIPA, GDPR, CCPA/CPRA, SOX, GLBA, the FTC Safeguards Rule, FCPA, FERPA, PCI DSS, the Copyright Act, CFAA, the Computer Security Act, a BAA, an IMA, or any other law, regulation, framework, contract, or certification program.

Projects MUST identify applicable legal, regulatory, contractual, security, privacy, records-management, and business obligations before implementation, integration, deployment, or production data access. When applicability or interpretation is uncertain, the responsible project owner MUST obtain guidance from an authorized legal, compliance, security, privacy, contractual, or business authority.

Engineering documentation MUST distinguish confirmed requirements from assumptions, recommendations, and unresolved questions.

## 3. Core Baseline Requirements

The following requirements apply across this document family:

- Sensitive data MUST be treated as a liability unless a documented business, legal, operational, or contractual requirement justifies its collection, storage, transmission, display, logging, or retention.
- Projects MUST identify regulated, protected, confidential, audit-sensitive, licensed, or otherwise sensitive information before implementation, integration, deployment, or production-data access.
- Applicable legal, regulatory, contractual, security, privacy, records-management, and business obligations MUST be identified before the design that depends upon them is finalized.
- Systems handling sensitive data MUST fail safely and MUST NOT disclose sensitive values through failure behavior.
- Sensitive data MUST NOT be written to logs, diagnostics, telemetry, screenshots, console output, temporary files, or exception messages unless explicitly required, approved, access-controlled, and documented.
- Production sensitive data MUST NOT be used in development, test, demo, or training environments unless explicitly approved and protected for that purpose.
- Secrets and credentials MUST NOT be stored in source control.
- Sample data committed to source control MUST be fake, synthetic, or confirmed non-sensitive.
- Imported or exported files involving external parties SHOULD trigger sensitive-data review.
- Copyrighted or licensed third-party materials MUST NOT be copied into a project unless usage rights are documented.
- Sensitive-data handling decisions SHOULD be documented close to the implementation.

Detailed requirements are authoritative in the applicable companion document.

## 4. Document Family

This standard is organized as a document family. This root document defines shared scope, baseline requirements, review questions, and navigation. Each companion document owns the detailed rules for a distinct responsibility:

- [Data Classification and Minimization Standards](compliance-and-sensitive-data/data-classification-and-minimization.md) — discovery, classification, PHI, PII, regulated data, confidential business data, classification drift, and minimum-necessary use.
- [Sensitive-Data Protection Controls](compliance-and-sensitive-data/protection-controls.md) — credentials and secrets, non-production data, masking, redaction, de-identification, tokenization, hashing, encryption, and data-type-specific safeguards.
- [Third-Party Data Exchange Standards](compliance-and-sensitive-data/third-party-data-exchange.md) — transmission, integrations, external processors and recipients, and completeness-versus-minimization boundaries.
- [Sensitive-Data Access, Audit, and Operations Standards](compliance-and-sensitive-data/access-audit-and-operations.md) — logging and diagnostics, authorization, tenant isolation, privileged and bulk access, auditability, and incident awareness.
- [Sensitive-Data Storage, Retention, and Disposal Standards](compliance-and-sensitive-data/retention-and-disposal.md) — persistence, backups, restoration, retention, and secure disposal.
- [Regulatory and Contractual Context](compliance-and-sensitive-data/regulatory-and-contractual-context.md) — regulatory sources, agreements, licensing, copyright, and other external obligations that shape engineering decisions.

Companion documents use local section numbering. Their numbers describe structure within that document and do not represent sections of a reconstructed monolithic standard.

## 5. Project Sensitive-Data Review Checklist

Before building or materially modifying a system, the project team should be able to answer:

- What sensitive, confidential, regulated, licensed, or audit-sensitive information is involved?
- Why is each category of data necessary?
- What legal, regulatory, contractual, security, privacy, records-management, and business obligations have been identified?
- Who is authorized to provide, access, change, export, and delete the data?
- Where does the data enter, flow, persist, replicate, appear, and leave the system?
- Which third parties, processors, subprocessors, intermediaries, and downstream recipients can receive or access it?
- Does an executed agreement require complete and accurate values, and how are those requirements reconciled with data minimization?
- Can the design avoid collecting or retaining any of it?
- Could logs, diagnostics, telemetry, screenshots, errors, filenames, URLs, or support tools expose it?
- Are secrets stored outside source control and capable of rotation and revocation?
- Are development, test, demo, and training materials synthetic or confirmed non-sensitive?
- Are redaction, masking, de-identification, tokenization, hashing, and encryption used according to their actual properties?
- Does the system fail safely when authorization, validation, encryption, transport, or integration requirements are not satisfied?
- Are retention, legal hold, archival, backup, and disposal behaviors documented?
- Are access and sensitive actions auditable without recording protected content?
- Are tenant, client, group, account, and record-level authorization boundaries enforced consistently across interactive, background, reporting, and integration paths?
- Are privileged, support, impersonation, emergency, and bulk operations separately authorized, bounded, and auditable?
- Are third-party code, fonts, images, documents, datasets, and other assets licensed for the intended use?
- Is there a known process for reporting suspected exposure, misuse, or control failure?
- Are unresolved assumptions assigned to an authorized owner before implementation, deployment, or production data access?

A checklist response does not certify compliance. Material risks, unknowns, and exceptions MUST be documented and resolved or explicitly accepted by an authorized owner.

## 6. Relationship to Other Standards Documents

This document family applies alongside the other Ichthus Development standards:

- [General Engineering Principles](principles.md) defines explicitness, stewardship, diagnostics, documentation, and APIs as contracts.
- [Source Formatting Standards](formatting.md) governs readable source and documentation formatting.
- [.NET Language Standards](dotnet.md) governs implementation details for .NET projects.
- [SQL and Database Standards](sql.md) governs database schema, query, and persistence design.
- [Data Format Standards](data-formats.md) governs serialization and external data representation.
- [Approved Libraries and Dependency Standards](approved-libraries.md) governs third-party code and dependency selection.
- [UI Standards](ui-standards.md) governs presentation and interaction design.
- [Accessibility Standards](accessibility.md) governs inclusive access to interfaces and content.
- [Language and Ecosystem Standards](languages.md) governs language-specific and framework-specific expectations.

When requirements overlap, the more specific documented requirement applies, but a project MUST NOT use specificity to weaken a legal, contractual, security, privacy, or data-protection obligation.

---

*Ichthus Development Engineering and Coding Standards exist to serve understanding, not fashion.*

© Gold Fish Bowl, LLC, DBA Ichthus Development

