# Free vs Pro

This page reflects the current access boundary in the extension implementation. It is intentionally practical: it focuses on which workflows you can rely on in Free mode and which workflows currently require Pro access.

## Included in Free

These workflows are part of the base editing experience:

- completion, hover, go to definition, and find references
- diagnostics, formatting, and code actions
- PHPUnit and Pest discovery in the Test Explorer
- Xdebug-based debugging
- Composer commands and include-path configuration
- interpreter management and PHP-version selection
- TODO tools

## Requires Pro

These workflows currently require Pro access or an active trial:

- Rename Symbol
- Generate Getter, Setter, and missing accessors
- Implement Missing Methods
- Code fixes from CF diagnostics
- Profile Current File
- Start Web Profiling
- Open Profiler and review profiling captures
- Debug inline values on the stopped line

Pro also adds completion polish by starring the strongest matches and preselecting the best suggestion.

## Quick matrix

| Workflow                         | Free         | Pro unlocks                                                           |
| -------------------------------- | ------------ | --------------------------------------------------------------------- |
| Code intelligence and navigation | Included     | Same core experience, plus starred completion suggestions             |
| Diagnostics and code actions     | Included     | Same core experience, plus Pro-only code fixes                        |
| Formatting                       | Included     | Same core experience                                                  |
| PHPUnit and Pest workflows       | Included     | Same core experience                                                  |
| Debugging                        | Included     | Inline debug values on the stopped line                               |
| Composer helpers and TODO tools  | Included     | Same core experience                                                  |
| Rename Symbol                    | Not included | Included                                                              |
| Accessor generation              | Not included | Generate getters, setters, and missing accessors                      |
| Implement Missing Methods        | Not included | Generate contract stubs for abstract/interface methods                |
| Profiling workflows              | Not included | Profile current file, start web profiling, and open profiler captures |

## Trial and activation states

The status bar communicates the current access state. Depending on your setup, you may see:

- Free
- Trial
- Pro
- Grace Period

Use `PhpThunder: Activate License` to open the license page and either start from your account or enter a license key directly.

## Related guides

- [Installation and activation](02-installation-and-activation.md)
- [Profiling](05-profiling.md)
- [Troubleshooting](09-troubleshooting.md)
