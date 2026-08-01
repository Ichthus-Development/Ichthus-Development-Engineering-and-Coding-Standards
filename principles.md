# Engineering Principles

## Guiding Principles

These principles override tooling trends, framework fashion, and external style guides.

1. **Clarity over convention**  
   Readability and semantic correctness take precedence over popularity.

2. **Explicit beats implicit**  
   Hidden behavior (magic defaults, inferred namespaces, silent conversions) is avoided wherever possible.

3. **Consistency over popularity**  
   A consistently applied rule is preferred over an externally fashionable one.

4. **APIs are contracts**  
   Public APIs are designed to be stable, intentional, and unsurprising across languages.

5. **Tooling serves the developer—not the reverse**  
   IDEs, analyzers, and frameworks must not dictate architectural correctness.

6. **Tool-Independent Readability**  
   Code should be readable and understandable without reliance on IDE features such as syntax highlighting, IntelliSense, or visual designers.

   Naming conventions, formatting, and structure are chosen to preserve semantic clarity when viewed in plain text editors or minimal environments.

   Tooling may enhance productivity, but it MUST NOT be required to understand intent.

   This principle informs [.NET naming and documentation](dotnet.md) and [SQL standards](sql.md).

These standards are informed by the principles articulated in the Gold Fish Bowl Babbagic Code.

## Terminology and Rule Severity

The following terms are used throughout this document:

- **MUST** — A mandatory requirement. Violations are considered defects.
- **SHOULD** — A strong recommendation. Deviations require justification.
- **MAY** — An optional guideline. Context-dependent.

These terms are used intentionally to enable future mechanical enforcement through tooling and to remove ambiguity during code review.

Lowercase must / should / may are descriptive prose only.  
Uppercase MUST / SHOULD / MAY define enforceable rules.

Usage of the terms "preferred" and "discouraged" indicate a strong default, not a prohibition.

For the purposes of this document, "public API" refers to any type, member, schema, or contract intended for consumption outside its defining assembly, project, or bounded context.

## Data Access and Object Design

- Centralized data access patterns are preferred.
- Lazy-loaded properties are acceptable when they improve performance or clarity.
- Attribute-based mapping and serialization control are preferred over convention-only approaches.

*Framework-specific abstractions must not leak into Core or domain contracts.*

## Type Semantics

- Prefer rich types (e.g., `FileInfo`) over primitive representations (e.g., file paths as strings) when behavior matters.

## Error Handling and Diagnostics

Diagnostics are defined as structured facts while logging is a consumer concern. As such, logging SHOULD be implemented according to the environment and business rules appropriate to the domain and SHOULD be implemented outside of `Core` or reusable libraries.

### Diagnostics over Exceptions

Libraries should:
- Prefer structured diagnostics over throwing exceptions
- Reserve exceptions for unrecoverable or truly exceptional conditions

Decision Boundary:
- Libraries emit diagnostics and continue execution where possible
- Consumers are responsible for interpreting diagnostics
- Escalation (e.g., throwing exceptions) is a policy decision, not a library default

This allows:
- Batch processing without hard failure
- Partial success scenarios
- Environment-specific strictness (development vs production)

Examples:

Avoid: throwing for expected, recoverable conditions

**VB.NET**

```vbnet
Throw New InvalidOperationException("Invalid record format")
```

**C#**

```csharp
throw new InvalidOperationException("Invalid record format");
```

Prefer: emitting diagnostics and continuing

**VB.NET**

```vbnet
diagnostics.Add(Diagnostic.Error(
    code: "INVALID_FORMAT",
    message: "Record format does not match expected schema"
))
```

**C#**

```csharp
diagnostics.Add(Diagnostic.Error(
    code: "INVALID_FORMAT",
    message: "Record format does not match expected schema"
));
```

### Severity Model

Diagnostics use a shared severity model:
- Information
- Warning
- Error
- Critical
- Fatal

Severity models should be consistent across all Ichthus Development projects.

## Conscious Deviations from Common Best Practices

As defined above, Ichthus Development intentionally deviates from some mainstream .NET conventions.

These deviations are:
- Deliberate
- Documented
- Consistently enforced

Examples include:
- ALL-CAPS acronyms instead of PascalCase acronyms
- Explicit namespace declarations
- SCREAMING_SNAKE_CASE constants
- Heavy use of diagnostics instead of exception-driven control flow
- Resistance to "magic" frameworks and opaque behavior

These choices exist to improve:
- Long-term maintainability
- Cross-language clarity
- Debuggability
- Architectural transparency

## Enforceability and Tooling Alignment

These standards are written with the expectation that they can be enforced through tooling where feasible (e.g., static analyzers, linters, CI validation).

Manual enforcement alone is considered insufficient for long-term consistency.

Where mechanical enforcement is not yet available, standards remain normative and are enforced through review.

Tooling enforcement does not replace human judgment but is intended to support consistency and early feedback.

Tooling enforcement supports these standards but does not override documented design intent or architectural judgment.

## Living Document

This document is expected to evolve.

Changes must:
- Be intentional
- Include rationale
- Be applied consistently across all Ichthus Development projects

[Return to the document guide](README.md#document-guide)

