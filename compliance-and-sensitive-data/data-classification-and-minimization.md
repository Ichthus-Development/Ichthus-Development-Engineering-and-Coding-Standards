# Data Classification and Minimization Standards

*Companion document in the Compliance and Sensitive Data Standards family*

This document defines how projects identify, classify, justify, and minimize sensitive data. It is authoritative for the detailed rules in its scope.

## 1. Data Classification

Every project that handles non-public information MUST define or adopt a data-classification model appropriate to its environment.

At minimum, the classification process MUST distinguish:

- Public information approved for unrestricted disclosure
- Internal information not intended for public distribution
- Confidential business or client information
- Restricted or regulated information requiring heightened controls
- Secrets and security-sensitive material requiring specialized handling

Classification MUST be based on the information's content, source, obligations, potential harm, and permitted use—not merely its filename, storage location, or technical format.

Projects MUST identify:

- What sensitive data is handled
- Why it is required
- Where it originates
- Where it flows
- Where it is stored or cached
- Who or what may access it
- How long it is retained
- How it is disposed of
- Which obligations govern it

Unknown data MUST NOT be treated as non-sensitive merely because it has not yet been classified. Imported files from clients, vendors, carriers, pharmacy benefit managers (PBMs), banks, schools, government systems, or other external partners SHOULD trigger sensitive-data review before processing or distribution.

Data-classification decisions SHOULD be documented close to the system design, contract, schema, integration, or implementation they govern.

### 1.1 Sensitive-Data Discovery and Classification Drift

Data classification MUST be reviewed when schemas, payloads, free-form fields, imports, integrations, reports, analytics, or business processes change materially.

A field or system originally classified as non-sensitive MUST be re-evaluated when its content, combination with other data, permitted use, or downstream distribution changes. Historical classification MUST NOT be treated as permanent evidence that current data is non-sensitive.

Projects SHOULD provide practical ways to discover unexpected sensitive content in databases, object storage, file shares, queues, indexes, logs, telemetry, exports, support bundles, and development artifacts. Discovery methods MUST themselves protect the values they inspect and MUST NOT create a new uncontrolled sensitive-data repository.

Data discovery SHOULD consider structured fields, free-form text, attachments, embedded documents, filenames, metadata, derived values, and combinations that permit correlation or re-identification.

Detected classification drift MUST trigger evaluation of existing access, storage, transmission, logging, retention, disposal, test-data, and contractual controls.

## 2. PHI, PII, and Regulated Data

Projects MUST identify whether PHI, PII, payment data, education records, financial records, employment records, government identifiers, biometric information, or other regulated data is involved.

Collection and processing MUST have a documented purpose and authorized basis. A convenient technical use is not, by itself, sufficient justification.

Systems MUST NOT infer that data is safe to disclose because individual fields appear harmless. Combinations of fields may identify a person, reveal protected facts, or permit re-identification.

Schemas, APIs, reports, exports, and integrations handling regulated data MUST make protection boundaries and permitted uses explicit. Hidden propagation of sensitive values through generic metadata, free-form fields, query strings, headers, filenames, or diagnostic context is prohibited.

Systems handling sensitive data MUST fail safely. Failure behavior MUST NOT disclose protected values, broaden access, bypass authorization, silently weaken encryption, or default to an insecure transport or storage path.

## 3. Confidential Business Data

Confidential business data includes non-public financial information, pricing, contracts, strategy, trade secrets, forecasts, internal investigations, security findings, proprietary methods, client information, employee information, and partner-provided materials.

Confidential business data MUST be collected, used, shared, and retained only for authorized purposes.

Access restrictions MUST follow the data across exports, reports, backups, support bundles, email attachments, collaboration platforms, and downstream integrations. Exporting data from a controlled application does not remove its classification or obligations.

Systems SHOULD avoid placing confidential information in filenames, URLs, object names, job names, queue names, or other metadata that may be broadly visible.

## 4. Minimum Necessary Data

Systems MUST collect, process, transmit, display, and retain only the minimum sensitive data necessary for the documented purpose.

Developers SHOULD prefer designs that avoid receiving sensitive data entirely when the required outcome can be achieved without it.

APIs, queries, reports, exports, and user interfaces SHOULD select explicit fields rather than entire records or unrestricted payloads. Convenience copies, speculative fields, and “future use” retention require documented justification.

Derived data, metadata, identifiers, and aggregates MUST be evaluated for sensitivity and re-identification risk. Reducing field count does not necessarily remove sensitivity.

---

[Return to the Compliance and Sensitive Data Standards](../compliance-and-sensitive-data.md)

