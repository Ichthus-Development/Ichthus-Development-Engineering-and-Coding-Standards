<p align="right"><img width="120" height="96" alt="Ichthus Development logo" src="https://github.com/user-attachments/assets/acf27b44-5bb3-474c-ac0b-3d4ac58d9bbe" /></p>

# Ichthus Development Engineering and Coding Standards

*Coding Conventions, Architectural Standards, and Design Rationale*

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-tomato?logo=creativecommons)](https://creativecommons.org/licenses/by/4.0/)

## Purpose

This repository defines the engineering principles, coding standards, architectural guidance, and deliberate deviations used across projects developed under **Ichthus Development**.

These standards promote clarity, consistency, maintainability, explicit design, and responsible software craftsmanship. They define boundaries, contracts, and expectations while leaving room for engineering judgment where multiple correct implementations exist.

They apply to application code, libraries, public APIs, data pipelines, database artifacts, user interfaces, documentation, scripts, and integration work produced under Ichthus Development.

## Relationship to the Gold Fish Bowl Ethos

Ichthus Development operates under **Gold Fish Bowl, LLC**. The organizational mission, vision, values, and ethical posture governing this work are defined in the [Gold Fish Bowl, LLC Ethos Collection](https://github.com/GoldFishBowlLLC/Babbagic-Code/blob/main/README.md).

This repository does not redefine those values. It translates their guiding intent into engineering standards and development practices.

## Guiding Approach

These standards are based primarily on established practices across software engineering, data engineering, and system design. Where Ichthus Development intentionally differs from a common convention, that difference must be explicit, consistently applied, and supported by rationale.

The foundational approach is summarized by these principles:

- Clarity over convention
- Explicit beats implicit
- Consistency over popularity
- APIs are contracts
- Tooling serves the developer, not the reverse
- Code must remain understandable without specialized tooling

See [Engineering Principles](principles.md) for the complete definitions and rule-severity model.

## Relationship to Industry Best Practices

Ichthus Development standards are based primarily on established industry best practices across software engineering, data engineering, and system design.

Where this collection defines deviations from commonly accepted practices, those deviations are intentional, experience-driven exceptions rather than wholesale rejections of industry guidance. Such exceptions are documented explicitly and exist to improve clarity, safety, cross-language interoperability, or long-term maintainability in real-world systems.

These standards apply to application code, libraries, APIs, data pipelines, and database artifacts produced under Ichthus Development.

## Non-Goals

These standards do not attempt to:

- Serve as an exhaustive language or framework reference
- Replace vendor documentation or authoritative specifications
- Prescribe every stylistic choice in every ecosystem
- Micromanage implementation where multiple sound approaches exist
- Enforce aesthetic preferences unrelated to clarity or correctness
- Require unrelated legacy code to be rewritten solely for conformance
- Guarantee performance, security, accessibility, or correctness without appropriate design, review, and testing
- Replace the organizational values defined by Gold Fish Bowl, LLC

Unless a project documents a stricter migration requirement, these standards apply prospectively to new work and to existing code when that code is materially modified.

## Document Families

Some standards cover broad domains whose responsibilities, review needs, and rates of change differ enough to justify companion documents. Such standards MAY be organized as a **document family**.

A document family MUST have a stable root document that defines its shared scope, baseline requirements, navigation, and relationship to the rest of these standards. Companion documents MUST each own a distinct area of detailed guidance, and each normative rule SHOULD have one authoritative home rather than being duplicated across the family.

Document families SHOULD be used when one or more of the following are true:

- The subject contains distinct engineering responsibilities that can be reviewed or adopted independently.
- Different parts of the subject require different expertise or evolve at materially different rates.
- A single document has become difficult to navigate or maintain without improving conceptual unity.
- Projects commonly need to reference one focused part of the standard without consuming the entire subject.

Companion documents use local section numbering. Their section numbers identify structure within that document; they do not imply a global reconstruction of an earlier monolithic standard.

The root document remains the canonical entry point for the family. Cross-document references SHOULD use document names and links rather than depending on section numbers outside the referenced document.

## Document Guide

Each document owns a defined area of responsibility. A rule should have one authoritative home; related documents link to that rule rather than restating it.

### [Engineering Principles](principles.md)

Defines the shared philosophy and architectural expectations governing all other standards, including rule terminology, public APIs, diagnostics, proportional resource use, conscious deviations, enforcement, and evolution.

### [.NET Standards](dotnet.md)

Defines standards for VB.NET, C#, and shared .NET APIs, including namespaces, naming, explicit typing, documentation, source organization, compiler diagnostics, and tooling attributes.

### [SQL and Database Standards](sql.md)

Defines formatting, naming, quoting, schema evolution, query design, migration ownership, and database-contract expectations.

### [Source Formatting Standards](formatting.md)

Defines cross-language expectations for readable source text and identifies formatting decisions that remain to be established.

### [Data Format Standards](data-formats.md)

Defines serialization, parsing, raw-input preservation, normalization, external naming, and traceability to external specifications.

### [Compliance and Sensitive Data Standards](compliance-and-sensitive-data.md)

Defines baseline engineering expectations for PHI, PII, regulated data, confidential business data, credentials, secrets, audit-sensitive records, copyrighted materials, and compliance-aware system design. This document does not provide legal advice or certify compliance, but requires sensitive-data and regulatory context to be identified and handled intentionally.

### [Approved Libraries and Dependencies](approved-libraries.md)

Defines how third-party dependencies are evaluated, approved, restricted, reviewed, and retired.

### [User Interface Standards](ui-standards.md)

Defines UI separation and framework-specific conventions, including WinForms control naming.

### [Accessibility Standards](accessibility.md)

Establishes the scope and planned structure for accessibility requirements as an engineering responsibility independent of any particular UI framework.

### [Language Governance](languages.md)

Identifies actively maintained languages and defines expectations for language-specific standards and transformed source.

## Standards Hierarchy

1. Legal, regulatory, contractual, security, and authoritative platform requirements take precedence.
2. The cross-cutting principles in `principles.md` apply throughout the collection.
3. Domain- and language-specific documents refine those principles within their stated scope.
4. Project-specific standards may add constraints or document justified exceptions, but must not silently contradict this collection.
5. When rules appear to conflict, follow the more specific rule and document the reason.

## Rule Terminology

- **MUST** — A mandatory requirement; a violation is considered a defect.
- **SHOULD** — A strong recommendation; deviations require justification.
- **MAY** — An optional, context-dependent practice.

Lowercase uses are descriptive prose unless the surrounding text clearly states otherwise. See [Rule Language and Definitions](principles.md#rule-language-and-definitions).

## Using These Standards

A new project should identify the documents relevant to its languages, data stores, interfaces, and deployment environment; adopt mechanical enforcement where practical; and record project-specific additions or justified deviations with rationale.

Tooling supports these standards but does not replace engineering judgment, review, testing, or documentation.

## Evolution and Contributions

These are living documents. Changes must be intentional, reviewed, rationale-driven, and applied consistently. Revisions should preserve continuity and include migration guidance when established consumers may be affected.

## License

This documentation is licensed under the [Creative Commons Attribution 4.0 International License](LICENSE).

---

*Ichthus Development Engineering and Coding Standards exist to serve understanding, not fashion.*

© Gold Fish Bowl, LLC, DBA Ichthus Development
