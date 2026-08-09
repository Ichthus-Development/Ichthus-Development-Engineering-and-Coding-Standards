# Sensitive-Data Protection Controls

*Companion document in the Compliance and Sensitive Data Standards family*

This document defines baseline controls for secrets, non-production data, and transformations used to protect sensitive information. It is authoritative for the detailed rules in its scope.

## 1. Credentials, Secrets, Tokens, Certificates, and Keys

Secrets and credentials MUST NOT be stored in source control. This includes passwords, API keys, access tokens, refresh tokens, session secrets, private keys, connection strings containing credentials, certificate private material, recovery codes, signing secrets, and production authentication artifacts.

Secrets MUST be stored and delivered through an approved secret-management mechanism appropriate to the environment.

Systems MUST:

- Restrict secret access to the minimum required identities and processes
- Separate secrets by environment and purpose
- Support rotation and revocation
- Avoid exposing secrets through command history, process arguments, build output, logs, diagnostics, telemetry, crash reports, or user interfaces
- Validate certificates and trust relationships explicitly
- Protect private keys from unauthorized export or disclosure

Public identifiers, certificate chains, and public keys MUST NOT be assumed secret; however, their integrity, provenance, and authorized use may still be security-sensitive.

Secret defaults, example credentials, and shared production accounts are prohibited. Development conveniences MUST NOT create implicit production credentials or bypass required authentication.

Suspected secret exposure MUST be treated as a security event. Removing a secret from the latest source revision is insufficient; the secret MUST be revoked or rotated, and repository history, build artifacts, caches, and downstream copies MUST be evaluated.

## 2. Test Data, Development Data, Demo Data, and Training Data

Production PHI, PII, credentials, tokens, keys, customer data, employee data, patient/member/dependent data, payroll data, benefit data, claims data, or regulated data MUST NOT be used in development, test, demo, or training environments unless explicitly approved and protected for that purpose.

Sample data committed to source control MUST be fake, synthetic, or confirmed non-sensitive.

Synthetic data SHOULD represent relevant formats, edge cases, relationships, and failure conditions without reproducing real people, accounts, credentials, or confidential records.

Changing names or a small number of obvious fields does not necessarily de-identify a production record. Test-data preparation MUST consider indirect identifiers, free-form text, embedded documents, metadata, filenames, dates, geographic information, and linked records.

Training materials, screenshots, videos, demonstrations, support examples, and documentation MUST be reviewed for sensitive information before distribution.

Non-production environments handling approved sensitive data MUST receive protections appropriate to the data, not weaker controls merely because the environment is labeled “test” or “development.”

## 3. Redaction, Masking, De-identification, Tokenization, Hashing, and Encryption

### 3.1 Control Selection Principle

Redaction, masking, de-identification, tokenization, hashing, and encryption MUST NOT be treated as interchangeable concepts.

- **Redaction** removes or replaces information so the protected value is not present in the resulting output.
- **Masking** obscures part or all of a displayed value while the underlying value may remain available elsewhere.
- **De-identification** reduces the ability to associate data with a person or entity according to defined criteria and risk analysis.
- **Tokenization** replaces a value with a token whose relationship to the original is maintained by a controlled system or mapping.
- **Hashing** produces a one-way digest but may remain vulnerable to guessing, lookup, correlation, or weak-input attacks.
- **Encryption** transforms data using cryptographic keys so authorized parties can recover it.

The selected control MUST match the intended threat, use, reversibility, retention, and disclosure requirements.

Masking MUST NOT be represented as removal. Hashing MUST NOT be represented as anonymization. Encryption MUST NOT be represented as deletion or as proof that access is authorized.

Control selection MUST begin with whether the system needs to receive or retain the sensitive value at all.

- If the original value is unnecessary, the system MUST NOT collect or retain it.
- If the original value must be recovered, approved encryption with controlled key management SHOULD be used.
- If a stable reference is required but recovery is unnecessary, approved tokenization or a purpose-specific keyed transformation SHOULD be considered.
- If only partial human recognition is required, the displayed value SHOULD be masked.
- If a value must be permanently absent from an output, it MUST be redacted rather than merely hidden by presentation logic.
- If data is used for analytics, research, training, or other secondary purposes, the project MUST define and approve the required de-identification method and re-identification risk.

The protection applied to a value MUST follow all copies and representations within scope, including database columns, indexes, exports, backups, caches, messages, reports, and logs.

### 3.2 Default Handling by Data Type

The following baselines apply unless a more specific, identified requirement imposes a stronger or different control:

| Data or use | Baseline engineering treatment |
|---|---|
| Original value is not required | Do not collect or retain it |
| Original value must be retrieved | Encrypt it using approved cryptography and controlled keys |
| Stable reference is required without routine disclosure | Tokenize it or use an approved purpose-specific keyed transformation |
| Password verification | Store a salted, costed password verifier; do not store a recoverable password |
| Verification of a high-entropy API token | Store a purpose-appropriate keyed or resistant verifier when token recovery is unnecessary |
| Partial human recognition | Mask the displayed value and protect the underlying value separately |
| Permanent removal from an output | Redact the value before the output is created or released |
| Secondary statistical or analytical use | Use an approved de-identification process with documented re-identification analysis |
| Transmission between systems | Use an authenticated, approved protected channel |

This table is a decision baseline, not a determination that a particular legal, regulatory, contractual, or framework requirement has been satisfied.

### 3.3 Payment Card and Financial Account Data

Payment card and financial account data SHOULD remain outside project scope when an approved provider, hosted payment flow, or tokenization service can meet the business requirement without the project receiving or storing the original value.

Payment-card security codes or values, PINs or PIN blocks, and full magnetic-stripe, chip-equivalent, or track data MUST NOT be retained after authorization. Encryption does not make prohibited post-authorization retention acceptable.

A full Primary Account Number (PAN) MUST NOT be stored unless an identified and approved business, legal, operational, or contractual requirement justifies retention. An authorized project handling stored PANs MUST apply the current, applicable PCI DSS requirements rather than relying solely on this document.

Stored PANs, bank-account numbers, payroll-account numbers, benefit-account numbers, and similarly sensitive financial identifiers MUST be rendered unreadable to unauthorized users and processes. Approved encryption or tokenization SHOULD be preferred when the original value must be recovered or referenced.

Financial identifiers MUST be masked by default in user interfaces, reports, exports, printouts, and support tools. Full-value display MUST require a documented business purpose, explicit authorization, deliberate user action, and appropriate auditability.

Masked, truncated, or “last four” values MUST NOT be used as passwords, authentication factors, or proof of identity. Such values may remain sensitive when combined with names, dates, balances, transactions, or other contextual information.

Routing numbers, bank identifiers, issuer identifiers, and similar values MUST be classified according to their actual use. A value that is publicly documented in one context may still contribute to fraud, correlation, or unauthorized disclosure in another.

### 3.4 Passwords, Credentials, and Verification Tokens

Passwords MUST NOT be stored in plaintext or using reversible encryption.

Password verifiers MUST use an approved password-hashing scheme with a unique salt and an appropriate, configurable cost factor. General-purpose fast hashes such as unkeyed SHA-family digests are not password-hashing schemes and MUST NOT be used alone for password storage.

The password-hashing algorithm, parameters, salt, version, and migration behavior MUST be explicit enough to support verification, work-factor increases, and future replacement without recovering the original password.

High-entropy API tokens, reset tokens, and similar bearer values SHOULD be stored using a purpose-appropriate keyed or resistant verifier when the original token does not need to be recovered. Tokens that must be presented to another system MUST instead be protected as recoverable secrets through an approved secret-management mechanism.

Passwords, credentials, and tokens MUST NOT appear in logs, diagnostics, telemetry, exception messages, URLs, screenshots, support bundles, or source-controlled samples.

### 3.5 PHI, PII, Government Identifiers, and Predictable Values

PHI, PII, government identifiers, member identifiers, claim identifiers, student identifiers, and other regulated or linkable values MUST be minimized and protected according to their classification, permitted use, and recovery requirements.

Predictable or low-entropy identifiers—including Social Security numbers, account numbers, telephone numbers, dates, postal codes, and many member or employee identifiers—MUST NOT be protected solely with an unkeyed hash when resistance to guessing, recovery, or correlation is required.

When equality matching is required without routine recovery, an approved tokenization system or purpose-specific keyed transformation MAY be used if collision behavior, key protection, rotation, access, and cross-system correlation risks are documented.

When the original value must be recovered, it SHOULD be encrypted using approved cryptography and keys stored separately from the protected data. Field-level, application-level, database-level, file-level, and device-level encryption protect different boundaries and MUST NOT be represented as equivalent.

Encryption at rest does not replace access control, data minimization, application security, retention, or auditability. A compromised or over-authorized application may access data after storage-layer decryption.

### 3.6 Display, Export, Search, and Correlation

User interfaces, reports, exports, and support tools SHOULD display the least sensitive representation that satisfies the authorized purpose.

Full-value reveal SHOULD be exceptional and SHOULD require:

- A documented business purpose
- Specific authorization
- Deliberate user action
- A limited display duration where practical
- Protection from unintended copying, caching, printing, or capture where practical
- An audit event that does not record the revealed value

Sensitive values MUST NOT be used as filenames, URLs, query-string parameters, queue names, job names, event names, correlation identifiers, or general-purpose search keys.

Indexes, search services, analytics platforms, and observability systems MUST be included in sensitive-data review. An encrypted source field may still be exposed through a plaintext index, materialized view, derived column, or search document.

Exports MUST preserve classification, authorization, masking, retention, and disposal requirements. The ability to export data MUST NOT imply authorization to disclose or retain it outside the source system.

### 3.7 Prohibited Substitutions and False Assurances

The following claims and substitutions are prohibited unless their stated conditions are actually satisfied:

- Masking MUST NOT be described as encryption, deletion, or redaction.
- Truncation MUST NOT be described as masking when digits have been permanently removed, and masking MUST NOT be described as truncation when the complete value remains stored.
- Hashing MUST NOT be described as anonymization or encryption.
- Encryption MUST NOT be described as access control, authorization, deletion, or compliance.
- Tokenization MUST NOT be described as eliminating risk when a mapping service or recoverable relationship remains.
- De-identification MUST NOT be claimed solely because direct identifiers were removed.
- Device, disk, or database encryption MUST NOT be claimed to protect data from every authorized application, administrator, query, export, or compromised runtime.
- A vendor's compliance statement, certification, or product label MUST NOT be treated as proof that the project's implementation, configuration, data flow, or use is compliant.

Custom cryptography is prohibited unless an exceptional, documented requirement justifies it and qualified security review approves the design. Approved, maintained cryptographic libraries and platform facilities SHOULD be used.

Key selection, storage, rotation, revocation, algorithm choice, nonce or initialization-vector handling, and failure behavior MUST be explicit where cryptography is implemented.

---

[Return to the Compliance and Sensitive Data Standards](../compliance-and-sensitive-data.md)

