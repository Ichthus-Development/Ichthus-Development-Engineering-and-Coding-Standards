# SQL and Database Development Standards

SQL is treated as a first-class programming language and is subject to the same clarity and maintainability standards as application code.

## Formatting and Readability

- SQL keywords MUST be written in UPPERCASE.
- Major clauses (`SELECT`, `FROM`, `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`) MUST begin on new lines.
- Each selected column SHOULD appear on its own line.
- Logical conditions SHOULD be vertically aligned for readability.

### Comments

SQL comments SHOULD explain non-obvious intent, external constraints, dialect-specific behavior, or deliberate deviations. Comments MUST NOT merely restate the statement.

For standalone, version-controlled SQL scripts:

- Single-line comments using `--` MAY be used when line boundaries are preserved.
- Block comments using `/* ... */` MAY be used for commentary spanning multiple lines or requiring explicit boundaries.
- Comments MUST NOT be used to disable executable SQL as a substitute for version control or explicit conditional behavior.

For SQL embedded in, constructed by, or generated from application code:

- Comments SHOULD generally be placed in the surrounding application source rather than inside the SQL text.
- Embedded SQL comments MUST NOT be relied upon to preserve required statement behavior.
- Single-line SQL comments using `--` MUST NOT appear in SQL that may be concatenated, flattened, minified, normalized, or generated without guaranteed line terminators.
- When a comment must be included in such SQL, an explicitly bounded block comment using `/* ... */` SHOULD be used when supported by the target dialect.
- The final emitted SQL SHOULD be tested or inspected when comments, conditional fragments, or source transformations could change its interpretation.
- Untrusted or sensitive values MUST NOT be inserted into SQL comments.
- Comments MUST NOT substitute for parameterization, diagnostics, structured query tagging, or documentation in the surrounding application source.

Rationale:

`--` is bounded by a line ending, not by the source-code line visible in an IDE. If SQL text is flattened or assembled without line terminators, a single-line comment may consume the remainder of the statement.

## Identifier Naming and Quoting

- Object names MUST be descriptive and domain-relevant.
- Avoid cryptic abbreviations unless they are domain-standard.
- Identifiers MUST NOT use reserved words when a clear, domain-relevant alternative exists.
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
- All identifiers MUST be quoted according to the target dialect. This is a blanket rule and applies even when a particular identifier could be resolved without quoting.
- Quoting MUST be applied consistently to schemas, database objects, columns, aliases, constraints, and other identifiers.
- The quoting form MUST match the target dialect:
  - ANSI SQL Standard: `"Identifier"`
  - PostgreSQL: `"Identifier"` (Double quotes preserve case; Unquoted names are automatically converted to lowercase)
  - SQL Server (T-SQL): `[Identifier]` (Double quotes work if `QUOTED_IDENTIFIER` is `ON`)
  - MySQL: `` `Identifier` ``
  - SQLite: `"Identifier"` or `` `Identifier` ``

Consistent quoting makes identifier handling habitual and prevents accidental reliance on implicit case folding, reserved-word interpretation, or engine-specific resolution behavior.

### Aliases and Correlation Names

- Column aliases MUST use the `AS` keyword.
- Table and source aliases SHOULD use the `AS` keyword where the target dialect supports it.
- Aliases MUST describe the domain object, source role, or computed value they represent.
- Positional aliases such as `a`, `b`, and `c` MUST NOT be used merely to distinguish sources by their order of appearance.
- Single-character aliases MUST NOT be used in the outermost query block or primary `SELECT`, `INSERT`, `UPDATE`, `DELETE`, or `MERGE` statement.
- A single-character alias MAY be used within a tightly scoped subquery or other intermediate query block only when its meaning is immediately apparent, it cannot be confused with another source, and a longer alias would not improve readability.
- Aliases in nested or intermediate query blocks MUST remain understandable when the block is read independently.
- Computed expressions MUST receive descriptive aliases when their results are exposed to a consumer.
- Aliases MUST NOT obscure the underlying domain concept merely to shorten a query.

### Table, Column, Key, and Relationship Names

- A database or bounded schema MUST use a consistent convention for singular or plural table names.
- Semantic clarity takes precedence over imposing one grammatical form across unrelated databases or domains.
- Column names SHOULD generally be singular because a column represents one value within a row.
- Primary-key columns SHOULD identify their domain entity rather than using `ID` by itself (for example, `CustomerID`, `ClaimID`, or `EDITransactionID`).
- A foreign-key column SHOULD retain the name of the referenced identifier when that name accurately describes its role.
- When an object references the same entity in multiple roles, each foreign-key column MUST include the role in its name (for example, `BillingAddressID`, `ShippingAddressID`, `CreatedByUserID`, or `ApprovedByUserID`).

PascalCase separates words within one logical entity. An underscore separates independently meaningful database entities when an identifier explicitly combines them.

Rules:

- Relationship tables SHOULD use a meaningful domain concept when the relationship is itself a domain entity (for example, `Enrollment`, `Assignment`, or `Membership`).
- When a relationship table combines entity names because no clearer domain concept exists, an underscore MUST separate those entity names (for example, `User_Role`, `Product_Category`, or `Claim_Dependent`).
- Foreign-key constraints MUST use the form `FK_<ReferencingObject>_<ReferencedObject>` (for example, `FK_Order_Customer` or `FK_Claim_Member`).
- When more than one relationship exists between the same objects, the foreign-key constraint name MUST include the distinguishing role (for example, `FK_Order_BillingAddress_Address` and `FK_Order_ShippingAddress_Address`).
- PascalCase MUST be retained within each entity or role name.
- Underscores MUST NOT be used merely as general word separators.
- Ordinary foreign-key columns MUST NOT use an underscore merely to separate the entity from `ID`; use `CustomerID`, not `Customer_ID`.

## Schema Design and Evolution

- Database schema is considered part of the public contract.
- Prefer additive, non-destructive schema changes.
- Breaking changes MUST be intentional and documented.

### Keys and Referential Integrity

- Every persistent relational table SHOULD have a primary key.
- A persistent table without a primary key MUST have a documented reason based on its data model or operational purpose.
- Natural, surrogate, and compound keys MAY be used when selected intentionally according to the identity, stability, and access requirements of the domain.
- Key selection MUST NOT be dictated solely by framework convention or implementation convenience.
- Foreign-key columns MUST use types compatible with the referenced key. Differences in length, precision, scale, collation, signedness, or other type characteristics MUST NOT create ambiguous or unsafe comparisons.

A foreign key represents a direct relationship that is valid in the domain. A foreign key MUST NOT be added merely because two tables can be associated or because a relationship might be convenient for a particular query.

When a valid direct relationship exists between persistent relational tables, it MUST normally be enforced by the database. Application validation MAY supplement database enforcement but MUST NOT be its only substitute.

Relationships MAY be chained through intermediary tables:

```text
Borrower -> Loan -> Collateral
```

In such a model, the database enforces the `Borrower`–`Loan` and `Loan`–`Collateral` relationships independently. `Collateral` MUST NOT receive a redundant foreign key to `Borrower` unless a separate, direct borrower–collateral relationship exists in the domain.

Many-to-many relationships MUST be represented through an explicit relationship table when modeled relationally:

```text
Borrower -> Borrower_Collateral -> Collateral
```

The relationship table MUST enforce a foreign key to each participating entity. It MUST also define a primary key or unique constraint that prevents duplicate relationship rows according to the domain rules. A relationship table MAY contain additional attributes when the relationship itself carries domain data.

### Referential Actions

Referential actions MUST be selected deliberately for each relationship. The database or tooling default MUST NOT be accepted without determining whether it matches the domain lifecycle.

- Restrictive behavior such as `NO ACTION` or `RESTRICT` SHOULD be the default when dependent data must not be removed or detached implicitly.
- `ON DELETE CASCADE` MUST be used only when the dependent row has no valid independent lifecycle and deletion of the parent is intended to delete the dependent data.
- `ON DELETE SET NULL` MUST be used only when the foreign-key column is nullable and loss of the relationship leaves a valid, meaningful domain state.
- Update cascades MAY be used when referenced key values are legitimately mutable and the cascade preserves the intended identity.
- Cascading behavior MUST NOT be used merely to simplify application cleanup.
- Destructive or relationship-breaking cascades MUST be documented close to the schema definition when their intent is not self-evident.

Reviews of referential actions MUST consider complete cascade paths, not only one relationship at a time. Chained cascades, multiple cascade paths, cycles, bulk effects, audit requirements, soft-deletion behavior, restoration, and downstream integrations MUST be evaluated before deployment.

When a requested referential action could delete, detach, or rewrite a materially larger set of data than the initiating operation makes obvious, that behavior MUST be treated as high impact and protected through appropriate authorization, diagnostics, testing, and operational safeguards.

### Nullability and Missing Data

Nullability MUST describe the valid states of the domain.

- A column MUST be `NOT NULL` when absence of its value would violate a business rule or make the persisted record invalid.
- A column SHOULD permit `NULL` when absence is a valid state and no stronger domain rule requires a value.
- `NOT NULL` MUST NOT be imposed merely to avoid null handling in application code, satisfy framework convenience, or reflect the contents of current sample data.
- Application validation SHOULD identify missing required values early and provide useful diagnostics, but database constraints MUST remain authoritative for persistent record validity.
- Required values MUST NOT receive fabricated defaults merely to satisfy a `NOT NULL` constraint.

`NULL` represents the absence of a value. It does not, by itself, identify why the value is absent.

The reason that a column permits `NULL` SHOULD be documented in the schema definition, migration, data dictionary, model documentation, or other authoritative design material when it is not self-evident. A separate status or reason column MUST be added only when the domain needs to distinguish among states such as unknown, not yet known, not applicable, withheld, unavailable, or removed.

Empty strings and `NULL` are not interchangeable:

- `NULL` means that no value is present.
- An empty string means that a textual value is present and contains zero characters, except where the target dialect explicitly treats empty strings as `NULL`.
- Empty or whitespace-only strings MAY be valid when supported by the domain.
- The responsible DBA or database engineer MUST determine whether empty, whitespace-only, and missing text values are distinct for the applicable data model.
- Values MUST NOT be silently trimmed, converted to `NULL`, or converted from `NULL` unless the normalization is an intentional and documented rule.

Sentinel values such as `1900-01-01`, `9999-12-31`, `-1`, `UNKNOWN`, or `N/A` MAY be used when required by a documented business rule, external contract, source-system convention, ETL/ELT process, staging model, or diagnostic purpose.

- Sentinel semantics MUST be explicit and documented.
- A sentinel MUST be valid for the column type and MUST NOT be confused with an ordinary domain value.
- Sentinel values MUST NOT be introduced merely to avoid nullable types or null-aware logic.
- ETL/ELT and staging processes SHOULD preserve source-system sentinel values when they are useful for traceability or diagnosis.
- Translation of a sentinel to `NULL`, or of `NULL` to a sentinel, MUST occur at a documented boundary and MUST preserve required provenance.
- Authoritative domain tables SHOULD use `NULL` for missing data unless a documented rule requires the sentinel to remain part of the authoritative representation.

SQL expressions MUST account for three-valued logic:

- Null comparisons MUST use `IS NULL` or `IS NOT NULL`, not equality or inequality operators.
- Predicates, joins, constraints, aggregates, concatenation, ordering, and set operations MUST be reviewed for their behavior when nullable values are present.
- `NOT IN` MUST NOT be used with a nullable value set unless its three-valued-logic behavior is explicitly intended and verified; `NOT EXISTS` SHOULD be considered when it expresses the intended semantics safely.

A nullable foreign key represents an optional relationship and MUST be used only when the unassociated state is valid in the domain. Nullability MUST NOT be used solely to conceal unresolved relationships, failed lookups, or incomplete processing.

Raw import, staging, and diagnostic structures MAY permit `NULL` or sentinel values that are invalid in authoritative domain tables. Validation and diagnostics MUST prevent invalid or incomplete records from crossing into the authoritative schema without an explicit exception.

Changing a column between nullable and non-nullable is a schema-contract change:

- Changing `NULL` to `NOT NULL` MUST include a strategy for identifying and resolving existing missing values.
- Changing `NOT NULL` to `NULL` MUST document why the invariant is being weakened.
- Adding a required column MUST include a valid population or migration strategy.
- A fabricated value MUST NOT be introduced solely to make a nullability migration succeed.

### Constraint and Index Names

Constraints and indexes on persistent, version-controlled schema objects MUST be named explicitly in their definition or creation when the target database supports named objects of that type.

Names MUST be deterministic, descriptive, and consistent across development, test, staging, and production environments. They MUST identify the object or role governed by the constraint or index sufficiently for migrations, deployment diagnostics, schema comparison, and operational troubleshooting.

The following prefixes MUST be used where the corresponding object is supported:

- Primary key constraint: `PK_`
- Foreign key constraint: `FK_`
- Unique constraint: `UQ_`
- Check constraint: `CK_`
- Default constraint: `DF_`
- Non-unique index: `IX_`
- Unique index: `UX_`

Examples:

```text
PK_Customer
FK_Order_Customer
UQ_Customer_EmailAddress
CK_Claim_ServiceDates
DF_Order_CreatedDate
IX_Claim_MemberID
UX_Customer_EmailAddress
```

The identifier rules for logical entities and roles apply to constraint and index names. PascalCase MUST be retained within a single entity or role name, while underscores MUST separate independently meaningful entities, roles, or indexed concepts.

Unnamed constraints or indexes MAY be used only when the object name has no material operational, diagnostic, migration, or maintenance value. This exception is generally limited to short-lived temporary objects, generated intermediate structures, or equivalent implementation details that are not managed as durable schema.

Convenience alone is not sufficient justification for leaving a persistent constraint or index unnamed.

## Query Intent

- Prefer clarity over cleverness.
- Use Common Table Expressions (CTEs) when they improve readability.
- Avoid deeply nested queries that obscure intent.

### Statement Layout

- Every complete SQL statement MUST end with a semicolon where the target dialect supports statement terminators.
- Each major clause MUST begin on a separate line.
- Each selected expression SHOULD appear on its own line except in short, trivial queries where combining expressions clearly improves readability.
- Nontrivial `AND` and `OR` conditions SHOULD begin on separate lines at a consistent indentation level.
- Expressions that mix `AND` and `OR` MUST use parentheses to make the intended precedence explicit.
- Indentation MUST communicate query structure, nesting, and ownership of predicates.
- SQL MUST NOT use right-aligned “river” formatting as a required layout convention.
- Alignment that depends on padding keywords or expressions to a shared character position SHOULD be avoided because it is brittle under ordinary editing.
- Limited local alignment MAY be used when it materially improves the readability of a stable block without obscuring its structure or creating excessive formatting churn.

### Selection, Insertion, and Result Order

- `SELECT *` MUST NOT be used in production queries, views, stored procedures, or application SQL.
- `SELECT *` MAY be used by explicitly schema-agnostic administrative, diagnostic, or development tooling when returning every available column is the documented intent.
- Existence checks SHOULD avoid retrieving unused column data.
- `INSERT` statements MUST provide an explicit target-column list.
- A query that depends on result order MUST include an explicit `ORDER BY`.
- `ORDER BY` expressions MUST identify columns, aliases, or expressions explicitly.
- Ordinal positions such as `ORDER BY 1` or `ORDER BY 2` MUST NOT be used.

Rationale:

An ordinal `ORDER BY` refers to the position of an expression in the select list rather than its meaning. Adding, removing, or reordering selected expressions can therefore change the result order without producing an error.

### Joins and Predicates

- Join types SHOULD be explicit (for example, `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, or `FULL JOIN`) when the target dialect supports them.
- Comma-separated implicit joins MUST NOT be used.
- Each join predicate MUST appear with the `JOIN` that it constrains.
- Predicates that determine how two sources relate MUST be placed in the applicable `ON` clause.
- Predicates that filter the combined result MUST be placed in the `WHERE` clause.
- Moving a predicate between `ON` and `WHERE` MUST be treated as a semantic change, particularly for outer joins.

### Query Constructs

- `BETWEEN`, `IN`, CTEs, subqueries, temporary tables, derived tables, and set operators such as `UNION` MUST be selected according to their semantics and the clarity of the resulting query.
- None of these constructs is universally preferred or prohibited.
- Range predicates MUST account for the inclusive boundaries of `BETWEEN`.
- Date and timestamp ranges SHOULD use explicit half-open boundaries when they represent contiguous periods (for example, values greater than or equal to the start and less than the following boundary).
- `UNION ALL` SHOULD be preferred over `UNION` when duplicate elimination is not required.
- A construct chosen primarily for performance SHOULD be supported by a representative query plan, measurement, documented platform behavior, or known operational constraint.

## SQL Location and Ownership

- Schema and migration SQL is authoritative and versioned
- Ad-hoc SQL in application code SHOULD be minimized
- Complex queries SHOULD be named, documented, or externalized

Rationale:  
SQL is code and deserves the same review, ownership, and traceability.

[Return to the document guide](README.md#document-guide)
