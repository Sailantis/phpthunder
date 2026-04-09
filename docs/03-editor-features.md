# Editor features

PhpThunder is primarily an editing toolchain. This page focuses on the workflows that matter during everyday PHP development.

## Code intelligence

PhpThunder provides the core IDE behaviors you expect in a PHP workspace:

- completion for global symbols, class members, and static access
- hover information for symbols and inferred types
- go to definition and find references
- import assistance when short names are ambiguous or missing
- PHPDoc-aware editing behavior

These workflows become more reliable once the project index is warm and the correct PHP version is selected for the folder.

## Diagnostics and quick fixes

PhpThunder publishes diagnostics for:

- parse and syntax problems
- type-analysis problems
- selected PHP version feature mismatches
- selected PHPDoc issues
- unused imports and unused private members

Quick fixes and source actions include:

- organize imports
- remove unused imports
- remove unused private members
- generate PHPDoc stubs
- pick an import candidate when multiple matches exist

If a project uses third-party code heavily, remember that vendor diagnostics are disabled by default. You can enable them with `phpThunder.diagnostics.enableVendor` when needed.

## Formatting

PhpThunder exposes formatter controls for:

- arrays
- parameters
- arguments
- match arms
- `if`, `foreach`, `for`, `while`, and `switch` syntax style
- maximum inline width

The formatter can preserve the existing style or enforce a more opinionated layout, depending on the setting values.

## TODO workflows

PhpThunder also includes TODO support inside VS Code.

Key commands:

- `PhpThunder: Focus TODOs`
- `PhpThunder: Refresh TODOs`
- `PhpThunder: Filter TODOs`
- `PhpThunder: Group TODOs`

This is useful when you want PhpThunder to act as both the PHP language layer and a lightweight project-navigation assistant.

## Composer helpers

For projects that lean on Composer, PhpThunder exposes command-palette helpers for:

- install
- update
- require
- dump-autoload
- validate

These commands complement the language server and make project maintenance easier from inside the editor.

## Related Pro workflows

Some workflows are intentionally documented elsewhere because they change the license story:

- [Profiling](05-profiling.md)
- [Free vs Pro](08-free-vs-pro.md)

## Next steps

- Continue with [Debugging](04-debugging.md) for Xdebug launch and attach flows.
- Continue with [Project configuration](07-project-configuration.md) for settings details.
- Continue with [Troubleshooting](09-troubleshooting.md) if the editor state does not match the project.
