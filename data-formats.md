# Data Format Standards

## Internal vs External Serialization Conventions

- Internal models should follow Ichthus Development naming conventions (PascalCase, ALL-CAPS acronyms).
- External serialization formats (e.g., JSON for public APIs) may adapt naming conventions as required for interoperability.
- Serialization naming differences must be explicit and intentional, not implicit or ad-hoc.

Rationale:
- Preserves internal clarity without sacrificing external compatibility.

## External Standards and Business Rule Traceability

When a design is driven by an external standard, specification, or third-party business rules, the origin of those constraints MUST be documented at the point of implementation.

This includes, but is not limited to:
- Industry standards (e.g., data interchange formats, protocol specifications, security standards)
- Third-party APIs or data contracts
- Regulatory or compliance requirements
- Vendor- or client-defined business rules

Documentation SHOULD clearly identify:
- The name of the standard or authority
- The relevant section, version, or rule identifier when applicable
- The reason the constraint exists
- Any known tradeoffs or deviations

This documentation MAY appear in:
- XML documentation comments (`<remarks>`, `<para>`)
- Inline comments when tightly coupled to a specific line or decision
- Referenced specifications using `<seealso>` or `<cref>` where appropriate

Examples:

**Implementations**

```vbnet
''' <remarks>
''' Implements delimiter detection as defined in
''' ANSI X12 §2.3.1 (Element Separators).
''' </remarks>
```

**Business Rules**

```vbnet
''' <remarks>
''' Behavior is driven by third-party settlement rules
''' provided by <VendorName>, revision 2024-03.
''' </remarks>
```

The goal is to ensure that non-obvious design decisions are not mistaken for accidental complexity or poor design.

Code that implements external constraints without documenting their origin is considered incomplete.

Refer to the definition of [public API](principles.md#terminology-and-rule-severity) and [Conscious Deviations](principles.md#conscious-deviations-from-common-best-practices) for further, detailed explanations.

## Data Handling Philosophy

- Prefer immutable or read-only data structures where practical
- Preserve raw input alongside parsed or transformed representations
- Never silently normalize or coerce data without documentation

[Return to the document guide](README.md#document-guide)

