# User Interface Standards

Accessibility complements these standards but remains an independent engineering responsibility. See [Accessibility Standards](accessibility.md).

## UI Control Naming Conventions (WinForms Only)

For Windows Forms applications, Ichthus Development adopts explicit control-prefix naming conventions.

This convention is **intentionally scoped to WinForms** and does not apply to WPF, MAUI, Blazor, or web-based UI frameworks.

### Rationale

WinForms relies heavily on:
- Event-handler wiring
- Partial classes
- Designer-generated code

Prefix-based control naming:
- Improves discoverability of event handlers
- Makes control intent obvious when navigating code
- Reduces ambiguity in large forms with many controls
- Speeds up maintenance in legacy or mixed-era codebases

### Convention

Controls SHOULD be prefixed according to their concrete type:

| Control Type | Prefix Example |
|-------------|----------------|
| `TextBox` | `txtUserName` |
| `Label` | `lblStatus` |
| `Button` | `cmdSubmit` |
| `CheckBox` | `chkIsEnabled` |
| `RadioButton` | `radOptionA` |
| `ComboBox` | `cboCountry` |
| `DataGridView` | `dgvResults` |
| `ListBox` | `lstItems` |
| `Panel` | `pnlMain` |
| `GroupBox` | `grpOptions` |

Prefixes MUST reflect the actual control type, not semantic intent.

> NOTE: This convention is retained for WinForms due to its event-driven, designer-generated architecture and is intentionally not extended to declarative or binding-based UI frameworks.

### Scope and Limitations

- This convention MUST NOT be applied outside WinForms.
- It MUST NOT be emulated in WPF, MAUI, Blazor, or XAML-based UI frameworks.
- Semantic naming without prefixes is preferred in modern UI frameworks that support strong binding and declarative layouts.

This convention exists to improve maintainability in WinForms, not to impose legacy patterns on modern UI development.

## UI Separation

Rules:
- No UI code in Core or shared libraries
- No `MessageBox`, dialogs, or UI callbacks in reusable logic
- Libraries must be safe for headless and server-side execution

Rationale:
- Enables batch processing
- Enables pipeline execution
- Prevents hidden coupling

## Framework-Specific Guidance

Framework- or platform-specific guidance (e.g., Blazor, MAUI, UI frameworks) is documented in project- or domain-specific companion specifications rather than in this core standards document.

[Return to the document guide](README.md#document-guide)

