# Sensitive-Data Storage, Retention, and Disposal Standards

*Companion document in the Compliance and Sensitive Data Standards family*

This document defines standards for sensitive-data persistence, backups, restoration, retention, and disposal. It is authoritative for the detailed rules in its scope.

## 1. Storage and Persistence

Sensitive data MUST be stored only in approved locations with controls appropriate to its classification and obligations.

Storage design MUST account for:

- Primary databases and file systems
- Backups, replicas, snapshots, and archives
- Caches and search indexes
- Queues, event streams, and dead-letter stores
- Temporary files and working directories
- Browser, application, and operating-system storage
- Reporting, analytics, and data-warehouse copies
- Developer workstations and support tooling

Sensitive data MUST NOT be persisted merely because persistence is convenient. Temporary persistence MUST have an explicit lifecycle and disposal behavior.

Encryption at rest SHOULD be used when required by classification, threat model, contract, platform policy, or applicable obligation. Encryption MUST NOT be used as a substitute for authorization, retention controls, secure configuration, or data minimization.

Storage locations, owners, access paths, backup behavior, recovery requirements, and retention rules SHOULD be documented.

### 1.1 Backups, Snapshots, Replicas, and Restoration

Backups, snapshots, replicas, archives, and disaster-recovery copies inherit the classification and obligations of their source data.

Sensitive production data MUST NOT be restored into development, test, demo, training, or support environments unless that use is explicitly approved and the destination provides protections appropriate to the data.

Backup and restoration design MUST account for:

- Access to backup media, consoles, keys, and recovery credentials
- Encryption and key availability during recovery
- Geographic, jurisdictional, contractual, and provider restrictions
- Retention, expiration, legal hold, and destruction
- Restoration testing without unnecessary exposure
- Reapplication of current access controls, security configuration, and patches
- Sensitive records that were deleted, corrected, restricted, or reclassified after the backup was created

Restoration MUST NOT silently reintroduce revoked credentials, obsolete permissions, deleted sensitive records, insecure configurations, or data whose permitted retention has expired.

Projects SHOULD document how restored data is reconciled with deletions, corrections, consent changes, legal holds, retention events, and other state changes that occurred after the restored copy was created.

## 2. Retention and Disposal

Sensitive data MUST have a documented retention basis and lifecycle.

Systems MUST NOT retain sensitive data indefinitely by default. Retention periods SHOULD be derived from legal, regulatory, contractual, operational, audit, and business requirements.

Disposal requirements apply to primary records and reasonably discoverable copies, including temporary files, exports, caches, queues, backups, snapshots, support packages, local working copies, and obsolete environments.

Deletion behavior MUST be described honestly. If immediate deletion from backups or immutable records is not technically possible, documentation MUST explain the actual expiration, isolation, restoration, and access behavior.

Legal holds, audit requirements, or records-management obligations MUST be identified before automated deletion is implemented or executed.

---

[Return to the Compliance and Sensitive Data Standards](../compliance-and-sensitive-data.md)

