# .NET Standards

## 1. Language Usage (VB.NET and C#)

Ichthus Development intentionally mixes **VB.NET** and **C#** within the same solution space.

### 1.1 Why VB.NET Exists Here

- Mature, expressive syntax for domain modeling
- Strong readability for business logic and data-heavy code
- Deep familiarity and long-term maintainability

### 1.2 Why C# Exists Here

- Broader ecosystem expectations
- Third-party library interoperability
- Modern tooling support

### 1.3 Cross-Language Rule

All public APIs MUST look natural, intentional, and idiomatic when consumed from both VB.NET and C#.

Language-specific features MUST NOT leak into shared contracts or public abstractions.

## 2. Namespace and Project Structure

### 2.1 Root Namespace Policy (VB.NET)

- **VB.NET Root Namespace is always blank**
- All namespaces are declared explicitly in code

Rationale:
- Eliminates VB/C# impedance mismatch
- Prevents "hidden" namespace concatenation
- Makes public API shape explicit and predictable

### 2.2 Core Namespaces

Namespaces ending in `.Core` represent:

- Dependency-safe contracts
- Fundamental domain models
- Interfaces and abstractions intended for long-term stability

Rules:
- `*.Core` MUST NOT depend on non-Core namespaces
- Implementations MAY depend on Core
- Core namespaces SHOULD be safe to reference from any project

Example:

```
Ichthus.Text.JSON.Core
```

For the purposes of this document, `Core` refers to both a conceptual architectural boundary and, where applicable, a physical project or assembly boundary.

### 2.3 Namespace Stability and Versioning

Namespaces are treated as part of the public API surface.

Rules:
- Public namespaces MUST be considered stable once released
- Moving a public type to a different namespace is a breaking change
- Namespace refactors require explicit versioning or migration strategy

Rationale:
- Namespaces communicate domain ownership and responsibility
- Consumers bind to namespaces implicitly through imports/usings
- Treating namespaces as disposable leads to silent downstream breakage

### 2.4 Namespace Semantics

Certain namespaces within the Ichthus root namespace carry **architectural meaning**, not just organizational grouping.

These namespaces communicate responsibility and intent and must be used consistently.

#### 2.4.1 `Core`

- Dependency-safe contracts
- Stable domain abstractions
- No external or implementation-specific dependencies

#### 2.4.2 `IO`

- Stream-based or persistence-oriented operations
- Files, sockets, buffers, or durable data sinks/sources
- Implies seek/read/write semantics

Examples:
- File readers/writers
- Network streams
- Memory-backed buffers

#### 2.4.3 `Console`

- Interactive, presentation-oriented output
- Human-facing input/output
- Not assumed to be durable or stream-seekable

Examples:
- Console writers
- Menu systems
- Interactive prompts

#### 2.4.4 `Diagnostics`

- Structured reporting of non-fatal conditions, validation issues, and system observations
- Not responsible for presentation or persistence
- May be consumed by logging, UI, telemetry, or test harnesses

Diagnostics represent facts; interpretation is the responsibility of the consumer.

#### 2.4.5 `Text`

- Textual data handling, parsing, tokenization, and transformation
- Format-aware but transport-agnostic
- Does not imply persistence, IO, or UI concerns

Examples:
- Parsers
- Tokenizers
- Format grammars

#### 2.4.6 `Policies`

- Behavioral rules and decision models
- No execution logic
- Used to influence how other components behave

Policies define *what should happen*, not *how it happens*.

#### 2.4.7 `Security`

- Security-sensitive utilities and abstractions
- Explicit, opt-in usage
- No silent encryption, hashing, or obfuscation

All security behavior must be visible at the call site.

#### 2.4.8 `Cryptography`

- Cryptographic primitives and transformations
- Explicit encryption, decryption, signing, verification, and hashing operations
- No implicit key management, storage, or policy decisions

Cryptographic operations must be:
- Explicit at the call site
- Opt-in
- Transparent in intent

#### 2.4.9 Other Domain Namespaces

Additional namespaces (e.g., `EDI`, `JSON`, `HTTP`) must define a clear responsibility boundary and should not overlap in purpose.

Namespaces such as `Utilities`, `Helpers`, or `Common` are discouraged and should be treated as refactoring waypoints, not architectural destinations.

Poorly defined namespaces must be corrected rather than compensated for with verbose type names.

## 3. Naming Conventions

### 3.1 Acronyms and Initialisms

**All acronyms are written in ALL CAPS.**

Examples:
- EDI
- XML
- JSON
- ASCII
- HL7

Rationale:
- Acronyms represent discrete semantic concepts
- Pascal-casing acronyms obscures meaning

Correct:
- `EDIParser`
- `XMLSerializer`

Incorrect:
- `EdiParser`
- `XmlSerializer`

### 3.2 General Naming Rules

- Public members: **PascalCase**
- No camelCase for public APIs
- Private members may follow language-idiomatic conventions
- Names should prioritize meaning over brevity

### 3.3 Constants

- Constants are declared using **SCREAMING_SNAKE_CASE**

Example:

**VB.NET**

```vbnet
Public Const MAX_RETRY_COUNT As Integer = 5
```

**C#**

```csharp
public const int MAX_RETRY_COUNT = 5;
```

Rationale:
- Visually distinguishes constants from variables
- Aligns with their immutable, global nature

### 3.4 Domain-Oriented Naming and Namespace Responsibility

Ichthus Development favors **domain-oriented namespaces** over redundant type prefixes.

#### 3.4.1 Namespace Carries Semantic Weight

When a type exists within a clearly defined domain namespace, **the namespace—not the type name—carries the primary semantic meaning**.

Redundant repetition of the domain name in type identifiers is discouraged.

Example:

**VB.NET**

```vbnet
Namespace Ichthus.EDI
    Public Interface IDelimiterDetector
End Namespace
```

**C#**

```csharp
namespace Ichthus.EDI
{
    public interface IDelimiterDetector
    {
    }
}
```

Preferred usage:

**VB.NET**

```vbnet
Dim detector As IDelimiterDetector
```

**C#**

```csharp
IDelimiterDetector detector;
```

Avoid:

```vbnet
IEDIDelimiterDetector
```

Rationale:
- Reduces visual noise
- Improves readability
- Encourages meaningful namespace design
- Prevents "stuttering" identifiers (`EDI.EDIDelimiterDetector`)

#### 3.4.2 When Domain Prefixes Are Acceptable

Domain prefixes may be retained only when the concept itself is cross-domain or taxonomy-like, and may reasonably appear outside its defining namespace.

Example:

**VB.NET**

```vbnet
Public Enum EDIFormat
    Unknown
    X12
    EDIFACT
End Enum
```

**C#**

```csharp
public enum EDIFormat
{
    Unknown,
    X12,
    EDIFACT
}
```

Rationale:
- `Format` alone is ambiguous across domains
- `EDIFormat` may appear in diagnostics, UI, metadata, or logging contexts
- Prefix improves clarity when consumed outside `Ichthus.EDI`

This exception is intentional and limited.

#### 3.4.3 Explicit Qualification Over Renaming

When name collisions occur across domains (e.g., `Writer`, `Reader`, `Parser`), explicit qualification or aliasing is preferred over renaming types.

Examples:

**VB.NET**

```vbnet
Imports EDIWriter = Ichthus.EDI.IO.Writer
Imports ConsoleWriter = Ichthus.Console.Writer
```

**C#**

```csharp
using EDIWriter = Ichthus.EDI.IO.Writer;
using ConsoleWriter = Ichthus.Console.Writer;
```

Rationale:
- Preserves clean, intention-revealing type names
- Avoids artificial suffixes (`EDIWriter`, `ConsoleWriter`)
- Keeps APIs natural and idiomatic
- Leverages language features instead of encoding context into names

*Type aliasing is considered a first-class language feature and an intentional part of Ichthus Development API consumption patterns.*

#### 3.4.4 Design Implication

This convention places higher importance on namespace architecture.

As a result:
- Namespaces must be intentional
- Namespace boundaries define responsibility
- Type names should remain concise, descriptive, and domain-local

*Poorly designed namespaces are not compensated for with verbose type names.*

## 4. Code Structure & Architectural Preferences

### 4.1 Variable Scope and Declaration Placement

- Local variables should be declared at the beginning of a method whenever practical.
- Variables scoped to blocks may be declared early and initialized to `Nothing` or an empty value when doing so improves readability without introducing unused state.
- Exceptions are permitted when early returns prevent unnecessary allocation.

Rationale:
- Improves scanability
- Reduces mid-method cognitive load

### 4.2 Type Safety and Explicit Typing

- Variables MUST be declared using the most specific, meaningful type available.
- Avoid using generic or ambiguous types (e.g., `Object`) when a concrete type exists.
- In C#, use of `var` SHOULD be limited to cases where the inferred type is immediately obvious and improves readability.
- In VB.NET, implicit typing that results in `Object` MUST be avoided.

Examples:

**VB.NET**

Avoid:

```vbnet
Dim result As Object = GetResult()
```

Prefer:

```vbnet
Dim result As ParseResult = GetResult()
```

**C#**

Avoid:

```csharp
var result = GetResult();
```

Prefer:

```csharp
ParseResult result = GetResult();
```

Exceptions are permitted only when:
- Required by reflection or late binding
- Imposed by external APIs or frameworks

Such exceptions MUST be documented inline with rationale.

### 4.3 Server-Side Technology Preference

- ASP.NET is the preferred platform for server-side logic and validation.
- Other technologies may be used only when constraints require it.

## 5. Code Documentation and Commenting

### 5.1 XML Documentation Comments

- XML documentation comments are required for all public types and members
- Internal members should be documented where intent is not obvious

All publicly visible members MUST be explicitly documented.

This includes:
- Public types
- Public methods
- Public properties (including read-only properties)
- Public fields and constants
- Enum types and individual enum values

Documentation is required even when behavior appears self-evident.

Public APIs are contracts, and contracts must describe intent, meaning, and usage—not just structure.

"Obvious" behavior is considered an implementation detail unless explicitly documented.

XML documentation comments SHOULD make use of:
- `<summary>` to describe intent
- `<param>` to explain parameter purpose
- `<returns>` where applicable
- `<remarks>` for constraints or edge cases
- `<seealso>` and `<cref>` for related types or specifications
- `<langword>` for language keywords

Documentation should explain *why a construct exists*, not merely restate syntax.

When documentation requires multiple conceptual paragraphs, `<para>` elements SHOULD be used instead of relying on line breaks or formatting conventions.

This ensures consistent rendering across IDEs and preserves semantic structure in generated documentation.

Examples:

**VB.NET (Without Documentation):**

```vbnet
Public Enum EDIFormat
    Unknown
    X12
    EDIFACT
```

**VB.NET (With Documentation):**

```vbnet
''' <summary>
''' Identifies the EDI interchange format.
''' </summary>
Public Enum EDIFormat
    ''' <summary>
    ''' Format could not be determined from the input data.
    ''' This value indicates detection failure, not a valid interchange.
    ''' </summary>
    Unknown

    ''' <summary>
    ''' ANSI ASC X12 format.
    ''' </summary>
    X12

    ''' <summary>
    ''' UN/EDIFACT format.
    ''' </summary>
    EDIFACT
End Enum
```

**C# (Without Documentation):**

```csharp
public enum EDIFormat
{
    Unknown,
    X12,
    EDIFACT
}
```

**C# (With Documentation):**

```csharp
/// <summary>
/// Identifies the EDI interchange format.
/// </summary>
public enum EDIFormat
{
    /// <summary>
    /// Format could not be determined from the input data.
    /// This value indicates detection failure, not a valid interchange.
    /// </summary>
    Unknown,

    /// <summary>
    /// ANSI ASC X12 format.
    /// </summary>
    X12,

    /// <summary>
    /// UN/EDIFACT format.
    /// </summary>
    EDIFACT
}
```

Rationale:
- Improves IntelliSense across languages
- Serves as living documentation
- Forces clarity of intent at design time

### 5.2 Inline Comments

Inline comments are reserved for:
- Explaining non-obvious intent
- Documenting deliberate deviations
- Clarifying constraints imposed by external systems

Inline comments MUST NOT:
- Restate obvious code behavior
- Duplicate XML documentation
- Serve as a substitute for clear naming or structure

### 5.3 Block Comments and Comment Scope

VB.NET does not support block comments.

This is considered an intentional design constraint, not a deficiency.

Standards for expressing multi-line commentary are:
- XML documentation comments (`'''`) for public and protected members
- Consecutive line comments (`'`) for internal commentary
- `<para>` elements for multi-paragraph XML documentation
- `#Region` blocks for structural grouping and navigability

Block-comment style disabling or masking of executable code is discouraged.

If code must be conditionally excluded, it SHOULD be removed or gated explicitly rather than commented out.

Rationale:
- Prevents accidental execution ambiguity
- Preserves line-by-line clarity
- Ensures comments remain readable in plain-text editors
- Avoids tooling- or formatting-dependent interpretation

### 5.4 Comment Philosophy

- Comments should explain why, not what
- Redundant comments are discouraged
- Historical or rationale-based comments are acceptable and encouraged

## 6. Code Organization

### 6.1 `#Region` (VB.NET) and `#region` (C#) Usage

- `#Region` blocks are used intentionally to organize:
  - Public properties
  - Private fields
  - Constructors
  - Public methods
  - Private methods
  - Event handlers

Rationale:
- Improves navigability in large files (code folding in IDE)
- Encourages logical grouping
- Aids long-term maintainability

## 7. Compiler and Tooling

### 7.1 Disabling and Suppressing Compiler Messages

Compiler warning suppression via `#Disable Warning` (VB.NET) or `#pragma warning disable` (C#) is disallowed.

Blanket or scope-based suppression obscures intent, hides future regressions, and undermines tooling effectiveness.

When a warning must be suppressed intentionally, targeted suppression via language-supported attributes (e.g., `<SuppressMessage>` / `[SuppressMessage]`) MAY be used only when:

- The specific rule being suppressed is named
- The suppression scope is limited to the smallest applicable symbol
- A clear justification is provided explaining why the rule does not apply

Suppressions without documented rationale are considered defects.

This follows the same principle as [explicit typing rules](#42-type-safety-and-explicit-typing): tooling must not be silenced to compensate for unclear design.

### 7.2 Debugger and IntelliSense Visibility Attributes

Attributes that influence debugger stepping or IntelliSense visibility (e.g., `<DebuggerStepThrough>`, `<EditorBrowsable>`, `<DebuggerBrowsable>`) MAY be used when they improve developer ergonomics without obscuring intent or correctness.

Such attributes are permitted only when:

- The underlying code is correct, well-tested, and intentional
- The attribute reduces noise rather than hiding complexity
- The member remains inspectable through source or reflection when necessary

> **Note:** In this context, "well-tested" implies the behavior has been verified through unit tests, integration tests, or long-standing production stability.

These attributes MUST NOT be used to:

- Conceal poorly designed APIs
- Hide complex or non-obvious logic
- Avoid addressing legitimate tooling warnings or design issues

When applied, the rationale for altering debugger or IntelliSense visibility SHOULD be evident from the surrounding context or documented inline if non-obvious.

## Related Standards

- [Serialization and external standards](data-formats.md)
- [WinForms control naming](ui-standards.md#ui-control-naming-conventions-winforms-only)
- [Engineering principles](principles.md)

[Return to the document guide](README.md#document-guide)

