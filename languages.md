# Language Governance

## Language-Specific Standards

Language-specific standards are defined only for languages actively used and maintained within Ichthus Development.

For other languages or ecosystems, this document defines architectural principles and expectations rather than prescriptive syntax rules.

## Languages with Source Transformation or Minification

Some languages and toolchains (e.g., JavaScript, TypeScript, CSS preprocessors) involve source-level transformation, bundling, or minification as part of their build or deployment process.

In such environments:
- Comments MUST NOT be relied upon to control runtime behavior.
- Comment-based masking or disabling of executable code is discouraged.
- Executable intent MUST be expressed through explicit language constructs, configuration, or build-time rules.

When minification or transformation is used:
- Source code MUST remain readable and intention-revealing prior to transformation.
- Tooling steps MUST NOT change program semantics beyond what is explicitly configured.
- Generated or transformed artifacts MUST NOT be treated as authoritative source.

Rationale:
- Comments are non-semantic and may be removed or altered by tooling.
- Readability and correctness must be preserved independently of build pipelines.
- Behavior should be explicit, reviewable, and enforceable at the source level.

[Return to the document guide](README.md#document-guide)

