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

The briefs in this section exist to help engineers and agentic workflows recognize when a source may warrant investigation. They are orientation aids, not substitutes for the controlling statute, regulation, contract, standard, authoritative guidance, or qualified interpretation.

### 2.1 Applicability, Authority, and Source Identification

Projects MUST identify which jurisdictions, entities, people, records, transactions, contracts, and environments bring a particular source into scope. Similar acronyms or subject matter do not establish applicability.

For every applicable source, documentation SHOULD identify:

- The full name and commonly used abbreviation
- The governing jurisdiction, organization, client, or contracting parties
- An authoritative source or controlling reference when one is publicly available
- The applicable version, effective date, contract date, or revision
- The responsible legal, compliance, security, privacy, contractual, or business authority
- The engineering requirements derived from that source
- Any unresolved interpretation or applicability question

Authoritative sources SHOULD be preferred over summaries, blogs, vendor checklists, search snippets, model memory, or other secondary explanations when determining applicability or deriving material requirements.

Source type SHOULD be distinguished where it affects authority. Examples include:

- **Statute or regulation** — enacted or promulgated legal authority.
- **Regulator or agency guidance** — official explanatory or enforcement material that may aid interpretation but does not necessarily have the same force as the controlling law or regulation.
- **External standard or framework** — a specification published by an authoritative standards body that may become mandatory through law, regulation, contract, policy, client direction, certification scope, or explicit project adoption.
- **Contractual source** — the executed agreement, amendment, addendum, statement of work, or other controlling instrument applicable to the parties.

A public link establishes provenance; it does not establish project applicability. The existence of an authoritative source MUST NOT be interpreted as a declaration that every project is governed by that source.

### 2.2 HIPAA and HITECH

**Brief:** The **Health Insurance Portability and Accountability Act (HIPAA)** and the HIPAA Privacy, Security, Breach Notification, and related Administrative Simplification Rules apply to defined covered entities and, for applicable provisions, business associates. The **Health Information Technology for Economic and Clinical Health Act (HITECH)** strengthened and expanded portions of the HIPAA privacy and security framework, including direct obligations for certain business associates. Health-related data is not automatically PHI merely because it concerns health.

**Authoritative sources:**

- [HHS Office for Civil Rights — HIPAA for Professionals](https://www.hhs.gov/hipaa/for-professionals/index.html)
- [HHS Office for Civil Rights — Covered Entities and Business Associates](https://www.hhs.gov/hipaa/for-professionals/covered-entities/index.html)
- [HHS Office for Civil Rights — HIPAA Security Rule](https://www.hhs.gov/hipaa/for-professionals/security/laws-regulations/index.html)
- [Electronic Code of Federal Regulations — 45 CFR Part 160](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-160)
- [Electronic Code of Federal Regulations — 45 CFR Part 164](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-164)

Engineering decisions may be affected by permitted uses and disclosures, minimum-necessary handling, administrative, physical, and technical safeguards, individual rights, business-associate relationships, auditability, incident handling, breach processes, retention, and data return or destruction.

Health-related information MUST NOT be labeled PHI solely because it concerns health. The project's authorized legal or compliance authority MUST determine whether HIPAA definitions and relationships apply.

### 2.3 Business Associate Agreements (BAAs)

**Brief:** A **Business Associate Agreement (BAA)** is a contractual instrument used in HIPAA-regulated relationships when the applicable covered-entity/business-associate requirements are met. It defines permitted and required uses and disclosures, safeguards, reporting, subcontractor obligations, termination behavior, and other contractual duties. A BAA is not a general-purpose certification that a product or organization is “HIPAA compliant.”

**Authoritative sources:**

- [HHS Office for Civil Rights — Covered Entities and Business Associates](https://www.hhs.gov/hipaa/for-professionals/covered-entities/index.html)
- [HHS — Model Business Associate Agreement](https://www.hhs.gov/sites/default/files/model-business-associate-agreement.pdf)

When a BAA applies, engineering teams MUST identify its permitted and required uses and disclosures, safeguards, incident and breach-reporting duties, subcontractor conditions, access and amendment support, audit or records obligations, termination provisions, and return or destruction requirements.

The actual executed agreement controls the contractual requirements. Sample language, prior-client terms, or a generic “HIPAA-compliant” product claim MUST NOT be substituted for review of the applicable agreement.

### 2.4 Personal Health Information Protection Act (PHIPA)

**Brief:** Ontario's **Personal Health Information Protection Act, 2004 (PHIPA)** establishes rules for collection, use, disclosure, safeguarding, access, correction, and other handling of personal health information within its scope. It is distinct from HIPAA and has its own definitions, regulated relationships, jurisdiction, and requirements.

**Authoritative sources:**

- [Ontario e-Laws — Personal Health Information Protection Act, 2004](https://www.ontario.ca/laws/statute/04p03)
- [Information and Privacy Commissioner of Ontario — Health Privacy](https://www.ipc.on.ca/en/resources/information-individuals/your-health-privacy-rights)

Engineering decisions may be affected by consent, authorized collection and use, disclosure restrictions, information practices, safeguards, access and correction, electronic health records, auditability, cross-border or external handling, and breach or notification obligations.

PHIPA and HIPAA MUST NOT be treated as interchangeable. A project may be subject to one, both, neither, or additional provincial, federal, contractual, or professional obligations.

### 2.5 General Data Protection Regulation (GDPR)

**Brief:** The **General Data Protection Regulation (GDPR), Regulation (EU) 2016/679**, governs processing of personal data within its material and territorial scope. It can apply to organizations established in the EU/EEA and, in specified circumstances, organizations outside the EU/EEA that offer goods or services to individuals there or monitor their behavior.

**Authoritative sources:**

- [EUR-Lex — Regulation (EU) 2016/679](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [European Commission — Legal Framework of EU Data Protection](https://commission.europa.eu/law/law-topic/data-protection/legal-framework-eu-data-protection_en)
- [European Commission — Application of the GDPR](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/application-gdpr_en)

Engineering decisions may be affected by lawful basis, transparency, purpose limitation, data minimization, accuracy, storage limitation, integrity and confidentiality, accountability, individual rights, processor and controller responsibilities, international transfers, privacy by design and default, and incident response.

Geographic hosting location alone MUST NOT be used to determine whether GDPR applies. Applicability and role assignments MUST be established by an authorized authority.

### 2.6 California Consumer Privacy Act and California Privacy Rights Act (CCPA/CPRA)

**Brief:** The **California Consumer Privacy Act (CCPA), as amended by the California Privacy Rights Act (CPRA)**, establishes privacy rights and obligations involving California consumers and covered businesses, service providers, contractors, and third parties. Applicability depends on statutory definitions, thresholds, relationships, exemptions, and the nature of the processing rather than on the mere presence of California residents in a dataset.

**Authoritative sources:**

- [California Legislative Information — California Consumer Privacy Act, Civil Code Title 1.81.5](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&chapter=&part=4.&lawCode=CIV&title=1.81.5)
- [California Privacy Protection Agency — Resources for Businesses](https://cppa.ca.gov/resources.html)
- [California Privacy Protection Agency — CCPA Regulations](https://cppa.ca.gov/regulations/)

Engineering decisions may be affected by notices, data inventories, consumer requests, access, deletion, correction, opt-out and preference signals, limitations on sensitive-personal-information use, purpose restrictions, service-provider and contractor terms, retention, cybersecurity obligations where applicable, and verification of requesting parties.

The CPRA amended the CCPA; project documentation SHOULD identify the current controlling statutory text and applicable regulations rather than treating CPRA as an unrelated standalone regime.

### 2.7 Sarbanes-Oxley Act (SOX)

**Brief:** The **Sarbanes-Oxley Act of 2002 (SOX)** governs aspects of public-company financial reporting, corporate responsibility, auditing, books and records, and internal control. Engineering relevance usually arises when systems, data transformations, reports, access paths, changes, or operational controls materially support in-scope financial reporting or related control evidence.

**Authoritative sources:**

- [U.S. Securities and Exchange Commission — Statutes and Regulations: Sarbanes-Oxley Act](https://www.sec.gov/rules-regulations/statutes-regulations)
- [U.S. Securities and Exchange Commission — Summary of SEC Actions and Related SOX Provisions](https://www.sec.gov/news/press/2003-89a.htm)

Engineering teams MUST identify which systems, interfaces, reports, transformations, and operational controls are considered in scope by the responsible financial, audit, legal, or compliance authority. A system MUST NOT be labeled “SOX compliant” solely because it has logging or access controls.

### 2.8 Gramm-Leach-Bliley Act and FTC Safeguards Rule (GLBA)

**Brief:** The **Gramm-Leach-Bliley Act (GLBA)** establishes privacy and safeguarding obligations for covered financial institutions, with regulatory and enforcement responsibilities distributed among multiple financial regulators. The **FTC Safeguards Rule, 16 CFR Part 314**, applies to financial institutions subject to FTC jurisdiction and requires an information security program for covered customer information.

**Authoritative sources:**

- [Federal Trade Commission — Gramm-Leach-Bliley Act](https://www.ftc.gov/legal-library/browse/statutes/gramm-leach-bliley-act)
- [Federal Trade Commission — GLBA Privacy and Security Guidance](https://www.ftc.gov/business-guidance/privacy-security/gramm-leach-bliley-act)
- [Federal Trade Commission — Safeguards Rule, 16 CFR Part 314](https://www.ftc.gov/legal-library/browse/rules/safeguards-rule)

Engineering decisions may be affected by security-program requirements, risk assessment, access control, encryption, monitoring, testing, incident response, disposal, service-provider oversight, privacy notices, information sharing, and protection of customer information or nonpublic personal information.

The responsible authority MUST determine whether the entity and activity fall within the jurisdiction of the FTC or another applicable financial regulator.

### 2.9 Foreign Corrupt Practices Act (FCPA)

**Brief:** The **Foreign Corrupt Practices Act (FCPA)** contains anti-bribery provisions and, for issuers within its accounting provisions, requirements concerning accurate books and records and internal accounting controls. Engineering relevance may arise in systems supporting payments, approvals, expenses, gifts, third-party relationships, financial records, audit trails, and control evidence.

**Authoritative sources:**

- [U.S. Department of Justice — Foreign Corrupt Practices Act Unit](https://www.justice.gov/criminal/criminal-fraud/foreign-corrupt-practices-act)
- [U.S. Department of Justice — FCPA Statutes](https://www.justice.gov/criminal/criminal-fraud/statutes-regulations)
- [DOJ and SEC — A Resource Guide to the U.S. Foreign Corrupt Practices Act](https://www.justice.gov/criminal/criminal-fraud/fcpa-resource-guide)
- [U.S. Department of Justice — Current FCPA Enforcement Guidelines](https://www.justice.gov/criminal/criminal-fraud/foreign-corrupt-practices-act/fcpa-guidelines)

Systems MUST preserve required record accuracy, authorization evidence, and traceability. Engineering teams MUST NOT implement hidden adjustments, undocumented overrides, or data transformations that undermine required books, records, or internal controls.

### 2.10 Family Educational Rights and Privacy Act (FERPA)

**Brief:** The **Family Educational Rights and Privacy Act (FERPA)** protects defined education records and personally identifiable information maintained by educational agencies and institutions receiving applicable U.S. Department of Education funding. It establishes rights involving access, amendment, and disclosure, subject to statutory and regulatory conditions and exceptions.

**Authoritative sources:**

- [U.S. Department of Education — FERPA](https://studentprivacy.ed.gov/ferpa)
- [U.S. Department of Education — Protecting Student Privacy](https://studentprivacy.ed.gov/)
- [Electronic Code of Federal Regulations — 34 CFR Part 99](https://www.ecfr.gov/current/title-34/subtitle-A/part-99)

Engineering decisions may be affected by access, amendment, disclosure, consent, legitimate educational interest, disclosure records, authentication of requesting parties, de-identification, directory information, and restrictions on redisclosure.

Student information MUST NOT be assumed subject to FERPA merely because it is used in an educational context; applicability depends on the institution, record, relationship, and governing authority.

### 2.11 Payment Card Industry Data Security Standard (PCI DSS)

**Brief:** The **Payment Card Industry Data Security Standard (PCI DSS)** is an industry security standard published by the PCI Security Standards Council for environments that store, process, or transmit payment account data within its defined scope. It is not a statute; applicability and validation obligations commonly arise through payment-card ecosystem relationships, contracts, acquiring-bank requirements, card-brand rules, and explicit organizational scope.

**Authoritative sources:**

- [PCI Security Standards Council — PCI DSS](https://www.pcisecuritystandards.org/standards/pci-dss/)
- [PCI Security Standards Council — Document Library](https://www.pcisecuritystandards.org/document_library/)

PCI DSS may materially affect architecture, scope reduction, segmentation, authentication, access, logging, testing, vulnerability management, cryptography, service-provider selection, and evidence collection.

Payment card data SHOULD be excluded from project scope when an approved external payment flow can meet the business requirement without the project receiving or storing it.

### 2.12 Copyright Act and Intellectual Property Obligations

**Brief:** U.S. copyright law is principally codified in **Title 17 of the United States Code** and governs rights in protected works including software, documentation, images, audiovisual material, and other creative works. Engineering teams must also account for licenses and contracts that grant, limit, or condition use beyond the baseline statutory rights.

**Authoritative sources:**

- [U.S. Copyright Office — Copyright Law of the United States, Title 17](https://www.copyright.gov/title17/)
- [U.S. Copyright Office](https://www.copyright.gov/)

Engineering decisions may be affected by copying, modification, distribution, display, derivative works, attribution, license compatibility, deployment, client delivery, and training use. See [Copyright, Licensing, and Third-Party Materials](#1-copyright-licensing-and-third-party-materials).

### 2.13 Computer Fraud and Abuse Act (CFAA)

**Brief:** The **Computer Fraud and Abuse Act (CFAA), 18 U.S.C. § 1030**, addresses specified unauthorized access and computer-related conduct. It is particularly relevant when engineering, automation, scraping, credential use, security testing, or research crosses authorization boundaries. Technical reachability is not authorization.

**Authoritative sources:**

- [U.S. Department of Justice — Justice Manual § 9-48.000, Computer Fraud and Abuse Act](https://www.justice.gov/jm/jm-9-48000-computer-fraud)
- [U.S. House Office of the Law Revision Counsel — 18 U.S.C. § 1030](https://www.govinfo.gov/link/uscode/18/1030)

Technical capability MUST NOT be treated as authorization. Testing, data acquisition, automation, and access to third-party systems MUST have documented permission and scope.

### 2.14 Computer Security Act and Federal Security Context

**Brief:** The **Computer Security Act of 1987** is historically important to U.S. federal information-security governance and helped establish federal security planning and standards responsibilities. It has been superseded by later federal information-security legislation and SHOULD NOT be treated as the current controlling authority for a modern federal system merely because its name appears in legacy documentation.

**Authoritative sources:**

- [NIST — Cybersecurity Legislation Overview](https://www.nist.gov/system/files/documents/2016/12/02/cybersecurity-commission-report-final-post.pdf)
- [GovInfo — Public Law 100-235, Computer Security Act of 1987](https://www.govinfo.gov/content/pkg/STATUTE-101/pdf/STATUTE-101-Pg1724.pdf)

Current federal projects may be governed by successor statutes, federal information-security requirements, agency policies, contractual clauses, authorization processes, and adopted standards. The current controlling sources MUST be identified for the specific system rather than inferred from historical terminology.

### 2.15 NIST Cybersecurity Framework and NIST SP 800-Series

**Brief:** The **NIST Cybersecurity Framework (CSF)** and **NIST Special Publication 800-series** provide cybersecurity risk-management, control, identity, incident, privacy, cryptographic, and system-security guidance. Their authority depends on context: some NIST publications are mandatory for particular federal systems or become mandatory through statute, regulation, policy, contract, authorization package, client direction, or explicit organizational adoption; others are advisory guidance.

**Authoritative sources:**

- [NIST — Cybersecurity Framework 2.0](https://www.nist.gov/cyberframework)
- [NIST Computer Security Resource Center — Special Publication 800-Series](https://csrc.nist.gov/publications/sp800)
- [NIST — Cybersecurity Framework 2.0 Publication](https://doi.org/10.6028/NIST.CSWP.29)

NIST publications do not automatically become mandatory merely because they are publicly available or widely respected.

Projects MUST identify the applicable publication, revision, profile, control baseline, implementation tier, cited section, or adopted requirement when NIST guidance is treated as normative.

### 2.16 Contractual Data and Information Agreements

**Brief:** Contracts can impose technical and operational obligations independently of statutes and external standards. For contractual requirements, the authoritative source is ordinarily the executed agreement and its controlling amendments, addenda, exhibits, statements of work, incorporated policies, or other documents made binding by the parties.

Examples include:

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
