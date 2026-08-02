# SQL and Database Development Standards

SQL is treated as a first-class programming language and is subject to the same clarity and maintainability standards as application code.

## Formatting and Readability

- SQL keywords MUST be written in UPPERCASE.
- Major clauses (`SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`) MUST begin on new lines.
- Each selected column SHOULD appear on its own line.
- Logical conditions SHOULD be vertically aligned for readability.

## Identifier Naming and Quoting

- Object names MUST be descriptive and domain-relevant.
- Avoid cryptic abbreviations unless they are domain-standard.
- Object names MUST conform to the [.NET naming conventions](dotnet.md#3-naming-conventions) when the SQL environment allows. Specifically:
  - [Acronyms and initialisms](dotnet.md#31-acronyms-and-initialisms) MUST be written in ALL CAPS
  - Object names (tables, columns, schemas, etc.) MUST be written in PascalCase
  - Schemas (when supported by the SQL environment) MUST be used as a part of the database design structure to define the domain in which the data resides similarly to how [namespaces carry primary semantic meaning](dotnet.md#341-namespace-carries-semantic-weight) in executable code
- Structural SQL object names represent domain truth and, as such, should read cleanly, descriptively, and without decoration. They MUST NOT contain prefixes or suffixes (`tbl_Customers`, `sch_Inventory`, `col_Address`, etc.)
- Functional SQL object names MUST include prefixes explicitly defining their usage and intent:
  - View: `vw_`
  - Stored Procedure: `usp_` (user-defined)
  - Scalar Function: `fn_`
  - Table-Valued Function: `tvf_`
  - Trigger: `tr_`
- Mixed-case or reserved identifiers MUST be quoted according to the target dialect:
  - ANSI SQL Standard: `"Identifier"`
  - PostgreSQL: `"Identifier"` (Double quotes preserve case; Unquoted names are automatically converted to lowercase)
  - SQL Server (T-SQL): `[Identifier]` (Double quotes work if `QUOTED_IDENTIFIER` is `ON`)
  - MySQL: `` `Identifier` ``
  - SQLite: `"Identifier"` or `` `Identifier` ``

Do not rely on implicit case folding or engine-specific quirks.

## Schema Design and Evolution

- Database schema is considered part of the public contract.
- Prefer additive, non-destructive schema changes.
- Breaking changes MUST be intentional and documented.

## Query Intent

- Prefer clarity over cleverness.
- Use Common Table Expressions (CTEs) when they improve readability.
- Avoid deeply nested queries that obscure intent.

## SQL Location and Ownership

- Schema and migration SQL is authoritative and versioned
- Ad-hoc SQL in application code SHOULD be minimized
- Complex queries SHOULD be named, documented, or externalized

Rationale:  
SQL is code and deserves the same review, ownership, and traceability.

[Return to the document guide](README.md#document-guide)

