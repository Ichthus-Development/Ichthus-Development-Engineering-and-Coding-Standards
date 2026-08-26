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

7. **Resource use follows delivered value**
   Spend resources in proportion to the value currently being delivered.

   Idle software should be substantially idle.

8. **Complexity belongs behind appropriate boundaries**  
   Necessary complexity SHOULD be handled by the layer best equipped to manage it rather than unnecessarily imposed on its consumers.

   Simplicity MUST NOT be manufactured by omitting correctness, validation, diagnostics, security, accessibility, maintainability, or other necessary engineering responsibilities.

9. **Evidence over status or consensus**  
   Material engineering conclusions SHOULD be justified by evidence, reproducibility, applicable requirements, and technical merit rather than authority, popularity, reputation, or vote count alone.

   Agreement is useful information, but consensus MUST NOT substitute for validation when correctness, safety, security, or other material risk requires independent evidence.

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

## Resource Efficiency

Ichthus Development software MUST NOT become bloatware. Features do not justify unnecessary or disproportionate consumption of CPU time, memory, storage, network bandwidth, battery power, startup time, background processes, or human attention created by the system's design.

Resource use MUST be proportional to the value currently being delivered. This standard applies to all Ichthus Development software and applies especially to long-running agents, services, tray applications, schedulers, daemons, background processors, and client software that remains resident for extended periods.

### Idle and Steady-State Behavior

Idle software should be substantially idle.

- Software that is not performing useful work SHOULD consume negligible CPU time and network bandwidth.
- Idle or steady-state software SHOULD NOT continually read or write storage, wake the processor, refresh unchanged state, or perform work whose result is not currently needed.
- Unusually high steady-state or idle resource consumption MUST be treated as a defect requiring investigation unless a concrete functional reason is documented.
- Features MUST be evaluated for startup, idle, and steady-state resource cost in addition to functional correctness and peak-load behavior.
- Resource measurements SHOULD be taken under representative conditions when the cost cannot be established reasonably through inspection.

### Background and Resident Work

Background activity MUST have a concrete, documented purpose.

This requirement applies to background services, polling loops, indexing, telemetry, synchronization, inventory, caches, queues, schedulers, watchers, helper processes, and permanently resident components.

- A background or resident process MUST NOT exist solely because it may be convenient for a possible future feature.
- Unnecessary startup applications, tray processes, helper processes, background workers, and permanently loaded modules MUST be avoided.
- Expensive or infrequently used capabilities SHOULD be activated on demand rather than kept continuously active.
- Heavyweight components SHOULD be loaded only when their capability is needed where practical.
- Background work SHOULD stop, suspend, or reduce its frequency when its purpose is no longer active.
- The lifetime, trigger, frequency, ownership, and shutdown behavior of significant background work SHOULD be explicit and reviewable.

### Events, Polling, and Scheduling

Event-driven behavior SHOULD be preferred over frequent polling when the relevant platform and data source provide a practical event mechanism.

Polling MAY be used when events are unavailable, unreliable, disproportionately complex, or inconsistent with an external contract. When polling is used:

- The interval MUST be appropriate to the actual timeliness requirement.
- The implementation SHOULD use backoff, coalescing, change detection, or suspension where those techniques reduce unnecessary work.
- Polling MUST NOT run more frequently merely to create the appearance of responsiveness.
- The reason for polling and the selected frequency SHOULD be documented when the resource cost is material or non-obvious.

### Bounded State and Data Collection

Software MUST NOT collect or maintain data merely because it might someday be useful.

- Collected and retained data MUST serve a current, documented functional, operational, contractual, or legal purpose.
- Background queues, caches, buffers, indexes, temporary data, diagnostic collections, and retained histories MUST be bounded by size, age, count, or another enforceable limit.
- Limit behavior MUST be intentional. Systems SHOULD define what is discarded, compacted, persisted, delayed, rejected, or surfaced diagnostically when a bound is reached.
- Caches MUST have a justified purpose and SHOULD be removable or reconstructible unless they are explicitly part of the durable data model.
- Telemetry and inventory collection MUST be scoped to information that is actively needed and MUST comply with the [Compliance and Sensitive Data Standards](compliance-and-sensitive-data.md).

### Frameworks, Dependencies, and Feature Cost

Frameworks and dependencies MUST be proportionate to the problem they solve.

- Disproportionately heavy frameworks, runtimes, services, or dependencies SHOULD NOT be introduced for trivial functionality when a simpler reasonable alternative exists.
- Dependency evaluation SHOULD consider runtime memory, startup cost, deployment size, background behavior, transitive components, and operational overhead in addition to developer convenience.
- A feature that requires continuous resource consumption MUST justify that continuous cost; the existence of the feature alone is not sufficient justification.
- Optional features SHOULD NOT impose substantial startup, resident-memory, storage, network, or background-processing cost on users who do not use them.

### Meaningful Optimization

Resource-conscious design MUST NOT devolve into premature micro-optimization.

- Engineering effort SHOULD focus on measured, observed, or reasonably foreseeable costs that materially affect users, systems, operations, or scalability.
- Maintainability, clarity, correctness, accessibility, security, diagnostics, and usability MUST NOT be sacrificed for negligible resource savings.
- Optimization SHOULD consider total cost to a correct outcome, including failures, retries, rework, operational burden, and human effort rather than optimizing one visible metric in isolation.
- Simpler implementation SHOULD be preferred when competing approaches have no material resource difference.
- Optimization that adds complexity SHOULD be supported by measurement, a documented constraint, or a clear operational requirement.

## Consumer-Oriented Simplicity

Interfaces, APIs, workflows, diagnostics, and operational controls SHOULD be designed around the needs and responsibilities of their consumers.

Internal implementation complexity MAY be justified when it materially reduces unnecessary complexity at a public, user, operator, or integration boundary while preserving correctness, observability, maintainability, and appropriate control.

A smaller implementation is not necessarily a simpler system. Fewer lines of code, fewer components, fewer configuration values, or fewer visible steps MUST NOT be treated as sufficient evidence that complexity has been reduced when equivalent or greater complexity has merely been transferred to callers, users, operators, support staff, or downstream systems.

Necessary design, validation, error handling, diagnostics, security, accessibility, maintainability, and workflow control MUST NOT be omitted merely to make an implementation appear simpler.

Refactoring SHOULD serve a concrete engineering purpose such as correctness, security, maintainability, testability, architectural clarity, reduced coupling, removal of meaningful duplication, or a demonstrated performance or operational need. Refactoring SHOULD NOT be required solely because another implementation is aesthetically preferred, fashionable, or merely possible.

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
