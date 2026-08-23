# Branding and Visual Identity Standards

> **Policy status:** Initial scope. This revision defines the core color palette and its implementation guidance only.

Branding should make Ichthus Development applications recognizable without compromising clarity, usability, or accessibility. This standard applies to the representation and use of brand colors in application themes, user interfaces, websites, documentation, and other visual artifacts produced under Ichthus Development.

## Canonical Core Color Palette

The following colors are the canonical core Ichthus Development brand colors:

| Brand Color | Hexadecimal Value | Semantic Resource | Intended Role |
|-------------|-------------------|-------------------|---------------|
| Ichthus Purple | `#6E52C7` | `BrandPrimary` | Primary brand expression and branded emphasis |
| Ichthus Gold | `#E1C363` | `BrandAccent` | Complementary accent and secondary emphasis |
| Ichthus Charcoal | `#333333` | `BackgroundDark` | Dark surfaces and backgrounds |

These hexadecimal values MUST be treated as the canonical source colors. Implementations MUST NOT silently substitute approximate values while representing the core palette.

## Semantic Resources and Implementation

Applications SHOULD define the core palette in a centralized theme or resource layer and reference semantic names such as `BrandPrimary`, `BrandAccent`, and `BackgroundDark` throughout UI code.

Raw hexadecimal values SHOULD NOT be scattered across views, components, styles, or application logic. They MAY appear in the authoritative palette definition, visual assets, build configuration, or tests that intentionally verify exact brand values.

Semantic resource names describe purpose rather than a specific framework or storage mechanism. Projects MAY map them to the theme, token, variable, resource, or style system appropriate to their platform.

## Derived Colors and Themes

Application-specific themes MAY derive additional shades, tints, or semantic resources from the core palette. Derived colors SHOULD remain visually consistent with the canonical colors and SHOULD be traceable to the source palette through theme definitions or documentation.

Light and dark themes MAY adapt surface, background, foreground, and emphasis usage while preserving a recognizable Ichthus Development identity. Theme adaptations SHOULD retain meaningful use of the core palette rather than requiring every canonical color to occupy the same role in every theme.

## Accessibility and Contrast

Accessibility and sufficient contrast SHOULD take precedence over rigidly forcing a brand color into a role where readability or interaction clarity would suffer.

When a canonical color does not provide sufficient contrast for a particular foreground, background, control state, or theme, the implementation SHOULD use an accessible derived color or alternate semantic resource. The canonical palette SHOULD remain recognizable elsewhere in the experience.

See [Accessibility Standards](accessibility.md) for the broader accessibility responsibility and [User Interface Standards](ui-standards.md) for framework and UI separation guidance.

This initial standard does not define typography, logo clear-space rules, iconography, marketing guidance, or a complete design system. Those subjects require separate, intentional review before adoption.

[Return to the document guide](README.md#document-guide)
