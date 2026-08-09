# Regulatory and Contractual Context

*Companion document in the Compliance and Sensitive Data Standards family*

This document identifies regulatory, contractual, licensing, and third-party contexts that may materially affect engineering decisions. It provides engineering context only; it is not legal advice, a legal interpretation, or a compliance certification.

## 1. Copyright, Licensing, and Third-Party Materials

Copyrighted code, fonts, icons, images, documents, datasets, or other third-party assets MUST NOT be copied into a project unless licensing and usage rights are documented.

Projects MUST identify the source, license, permitted use, attribution requirements, redistribution conditions, modification rights, and material restrictions for incorporated third-party works.

Public availability, technical accessibility, or the ability to copy material does not establish permission to use it.

Generated, purchased, client-provided, vendor-provided, and open-source materials MUST be reviewed according to their actual terms and provenance. License obligations SHOULD remain traceable to the files, packages, assets, or deliverables they govern.

Confidentiality and copyright are distinct. Permission to access a work does not necessarily grant permission to copy, modify, redistribute, publish, or use it for training.

## 2. Regulatory and Compliance Context

The following contexts may affect engineering decisions. This list is neither exhaustive nor a determination that a particular authority applies.

### 2.1 Applicability and Source Identification

Projects MUST identify which jurisdictions, entities, people, records, transactions, contracts, and environments bring a particular source into scope. Similar acronyms or subject matter do not establish applicability.

For every applicable source, documentation SHOULD identify:

- The full name and commonly used abbreviation
- The governing jurisdiction, organization, client, or contracting parties
- The applicable version, effective date, contract date, or revision
- The responsible legal, compliance, security, privacy, contractual, or business authority
- The engineering requirements derived from that source
- Any unresolved interpretation or applicability question

### 2.2 HIPAA and HITECH

The **Health Insurance Portability and Accountability Act (HIPAA)** and **Health Information Technology for Economic and Clinical Health Act (HITECH)** may affect covered entities, business associates, and systems that create, receive, maintain, or transmit PHI or electronic PHI.

Engineering decisions may be affected by permitted uses and disclosures, minimum-necessary handling, administrative, physical, and technical safeguards, individual rights, business-associate relationships, auditability, incident handling, breach processes, retention, and data return or destruction.

Health-related information MUST NOT be labeled PHI solely because it concerns health. The project's authorized legal or compliance authority MUST determine whether HIPAA definitions and relationships apply.

### 2.3 Business Associate Agreements (BAAs)

A **Business Associate Agreement (BAA)** is a contractual instrument associated with HIPAA-regulated relationships; it is not a separate statute or general-purpose compliance certificate.

When a BAA applies, engineering teams MUST identify its permitted and required uses and disclosures, safeguards, incident and breach-reporting duties, subcontractor conditions, access and amendment support, audit or records obligations, termination provisions, and return or destruction requirements.

The actual executed agreement controls the contractual requirements. Sample language, prior-client terms, or a generic “HIPAA-compliant” product claim MUST NOT be substituted for review of the applicable agreement.

### 2.4 Personal Health Information Protection Act (PHIPA)

Ontario's **Personal Health Information Protection Act, 2004 (PHIPA)** may affect health information custodians, agents, service providers, and systems that collect, use, disclose, retain, or dispose of personal health information within its scope.

Engineering decisions may be affected by consent, authorized collection and use, disclosure restrictions, information practices, safeguards, access and correction, electronic health records, auditability, cross-border or external handling, and breach or notification obligations.

PHIPA and HIPAA MUST NOT be treated as interchangeable. A project may be subject to one, both, neither, or additional provincial, federal, contractual, or professional obligations.

### 2.5 General Data Protection Regulation (GDPR)

The **General Data Protection Regulation (GDPR)** may affect processing of personal data connected to the European Union or European Economic Area according to its territorial and material scope.

Engineering decisions may be affected by lawful basis, transparency, purpose limitation, data minimization, accuracy, storage limitation, integrity and confidentiality, accountability, individual rights, processor and controller responsibilities, international transfers, privacy by design and default, and incident response.

Geographic hosting location alone MUST NOT be used to determine whether GDPR applies. Applicability and role assignments MUST be established by an authorized authority.

### 2.6 California Consumer Privacy Act and California Privacy Rights Act (CCPA/CPRA)

The **California Consumer Privacy Act (CCPA), as amended by the California Privacy Rights Act (CPRA)**, may affect businesses, service providers, contractors, third parties, and systems handling personal information or sensitive personal information within its scope.

Engineering decisions may be affected by notices, data inventories, consumer requests, access, deletion, correction, opt-out and preference signals, limitations on sensitive-personal-information use, purpose restrictions, service-provider and contractor terms, retention, and verification of requesting parties.

The CPRA amended the CCPA; project documentation SHOULD identify the current controlling text and regulations rather than treating CPRA as an unrelated standalone regime.

### 2.7 Sarbanes-Oxley Act (SOX)

The **Sarbanes-Oxley Act (SOX)** may affect systems supporting financial reporting, books and records, internal controls, change management, record integrity, access, approvals, evidence, and audit processes.

Engineering teams MUST identify which systems, interfaces, reports, transformations, and operational controls are considered in scope by the responsible financial, audit, legal, or compliance authority. A system MUST NOT be labeled “SOX compliant” solely because it has logging or access controls.

### 2.8 Gramm-Leach-Bliley Act and FTC Safeguards Rule (GLBA)

The **Gramm-Leach-Bliley Act (GLBA)** and **FTC Safeguards Rule** may affect covered financial institutions and systems handling customer information or nonpublic personal information.

Engineering decisions may be affected by security-program requirements, risk assessment, access control, encryption, monitoring, testing, incident response, disposal, service-provider oversight, and protection of customer information.

The responsible authority MUST determine whether the entity and activity fall within the relevant regulator's jurisdiction.

### 2.9 Foreign Corrupt Practices Act (FCPA)

The **Foreign Corrupt Practices Act (FCPA)** may affect systems supporting books, records, internal accounting controls, approvals, payments, gifts, expenses, third-party relationships, and audit trails.

Systems MUST preserve required record accuracy, authorization evidence, and traceability. Engineering teams MUST NOT implement hidden adjustments, undocumented overrides, or data transformations that undermine required books, records, or internal controls.

### 2.10 Family Educational Rights and Privacy Act (FERPA)

The **Family Educational Rights and Privacy Act (FERPA)** may affect education records and personally identifiable information maintained by covered educational agencies, institutions, or parties acting on their behalf.

Engineering decisions may be affected by access, amendment, disclosure, consent, legitimate-interest limitations, disclosure records, authentication of requesting parties, de-identification, and restrictions on redisclosure.

Student information MUST NOT be assumed subject to FERPA merely because it is used in an educational context; applicability depends on the institution, record, relationship, and governing authority.

### 2.11 Payment Card Industry Data Security Standard (PCI DSS)

The **Payment Card Industry Data Security Standard (PCI DSS)** is an industry standard that may apply contractually when payment card data is stored, processed, or transmitted.

PCI DSS may materially affect architecture, scope reduction, segmentation, authentication, access, logging, testing, vulnerability management, cryptography, service-provider selection, and evidence collection.

Payment card data SHOULD be excluded from project scope when an approved external payment flow can meet the business requirement without the project receiving or storing it.

### 2.12 Copyright Act and Intellectual Property Obligations

**Copyright law and applicable licenses** may affect software, fonts, icons, images, documentation, datasets, audiovisual works, models, and other third-party assets.

Engineering decisions may be affected by copying, modification, distribution, display, derivative works, attribution, license compatibility, deployment, client delivery, and training use. See [Copyright, Licensing, and Third-Party Materials](#1-copyright-licensing-and-third-party-materials).

### 2.13 Computer Fraud and Abuse Act (CFAA)

The **Computer Fraud and Abuse Act (CFAA)** may matter when engineering activity involves authorization boundaries, access to computers or accounts, security testing, automation, scraping, credential use, or activity beyond granted permission.

Technical capability MUST NOT be treated as authorization. Testing, data acquisition, automation, and access to third-party systems MUST have documented permission and scope.

### 2.14 Computer Security Act and Federal Security Context

The **Computer Security Act of 1987** provides historical context for federal information-security planning, training, and standards.

Current federal projects may be governed by successor statutes, federal information-security requirements, agency policies, contractual clauses, authorization processes, and adopted standards. The current controlling sources MUST be identified for the specific system rather than inferred from historical terminology.

### 2.15 NIST Cybersecurity Framework and NIST SP 800-Series

The **NIST Cybersecurity Framework (CSF)** and **NIST Special Publication 800-series** provide risk-management, control, identity, incident, privacy, cryptographic, and system-security guidance.

NIST publications do not automatically become mandatory merely because they are publicly available or widely respected. They may become required through law, regulation, policy, contract, client direction, security authorization, or explicit project adoption.

Projects MUST identify the applicable publication, revision, profile, control baseline, implementation tier, or cited section when NIST guidance is treated as normative.

### 2.16 Contractual Data and Information Agreements

Contracts may impose requirements independently of, or in addition to, statutes and external standards. Examples include:

- Information Management Agreements (IMAs)
- Data Use Agreements (DUAs)
- Data Sharing Agreements (DSAs)
- Information Security Agreements (ISAs)
- Non-Disclosure or Confidentiality Agreements (NDAs)
- Service-level agreements and security addenda
- Client, vendor, carrier, PBM, bank, school, or government data-exchange agreements

The acronym **IMA** does not have one universal legal or industry meaning. A project referring to an IMA MUST record the agreement's full title, parties, effective version, scope, and controlling provisions.

Engineering teams MUST translate applicable contractual terms into traceable requirements for data use, access, integration, safeguards, logging, audit, incident notice, subcontractors, retention, return, destruction, licensing, and termination. Contract names and compliance labels MUST NOT substitute for review of the executed terms.

Projects MUST identify the specific obligations, versions, contracts, policies, and responsible authorities that govern their work. References to an acronym or framework MUST NOT be treated as a substitute for an applicable requirement, control, or approved interpretation.

Compliance-sensitive implementations SHOULD cite the governing requirement or documented business rule close to the relevant design or code, consistent with [External Standards and Business Rule Traceability](../data-formats.md#external-standards-and-business-rule-traceability).

---

[Return to the Compliance and Sensitive Data Standards](../compliance-and-sensitive-data.md)
