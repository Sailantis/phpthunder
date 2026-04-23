# Editor features

PhpThunder is first and foremost an editing toolchain. This page covers the workflows that matter during everyday PHP development — from the first keystroke to the final commit.

## At a glance

| Feature                      | What it does                                                             |
| ---------------------------- | ------------------------------------------------------------------------ |
| Code intelligence            | Completion, hover, go-to-definition, find references, import suggestions |
| Diagnostics                  | Parse errors, type problems, version mismatches, unused code             |
| Quick fixes & source actions | Organize imports, generate PHPDoc, add use statements, remove dead code  |
| Formatting                   | Configurable style for arrays, parameters, control structures, and more  |
| TODO panel                   | Track and navigate `TODO`, `FIXME`, and similar comments project-wide    |
| Composer helpers             | Run install, update, require, and dump-autoload from the command palette |

## Code intelligence

PhpThunder provides the core IDE behaviors expected in a well-equipped PHP workspace.

### Completion

As code is entered, PhpThunder suggests global symbols (classes, functions, constants), class members, static access, and namespaced identifiers. The suggestions include method signatures, property types, and PHPDoc summaries, keeping parameter names close at hand.

> **Example:** Start typing `new Http` in a Laravel project and PhpThunder completes to `Illuminate\Http\Request`, adding the `use` statement at the top of the file if it's not already there.

<!-- MEDIA: GIF of completion with auto-import in a controller -->

> 📸 _Coming soon: GIF of completion and auto-import in a real controller._

### Hover

Hover over any symbol to see its type signature, return type, parameters, and PHPDoc — including documentation from Composer dependencies. No need to leave the current file.

<!-- MEDIA: screenshot of hover showing type + PHPDoc -->

> 📸 _Coming soon: screenshot of hover documentation on a method._

### Go to definition and find references

`F12` jumps to the definition of any symbol. `Shift+F12` (or right-click → Find All References) shows everywhere a symbol is used, across the entire project, including `vendor/` when vendor analysis is enabled.

### Import assistance

When a short class name cannot be resolved, PhpThunder offers to add the missing `use` statement. When multiple candidates exist (e.g., both `App\Request` and `Illuminate\Http\Request`), it shows a picker.

> **Tip:** `PhpThunder: Organize Imports` removes unused `use` statements and sorts the remaining ones. Bind it to a key or run it as a source action on save.

## Diagnostics and quick fixes

PhpThunder publishes diagnostics for:

- **Parse and syntax problems** — caught during typing, no save needed
- **Type analysis** — mismatched argument types, wrong return types, undefined properties
- **PHP version mismatches** — using PHP 8.1 named arguments in a project targeting 8.0
- **PHPDoc issues** — incorrect `@param` types, missing `@return` annotations
- **Unused imports** — `use` statements that are never referenced in the file
- **Unused private members** — private properties and methods that are never accessed

Quick fixes and source actions are available from the lightbulb (💡) or via `Ctrl+.`:

- **Organize imports** — sort and remove unused `use` statements
- **Remove unused imports** — surgical removal without touching ordering
- **Remove unused private members** — clean up dead code in a class
- **Generate PHPDoc stub** — scaffold a `/** */` block for any method or property
- **Pick import candidate** — resolve ambiguous short names with a picker

> **Note:** Vendor file diagnostics are off by default to keep the noise level low. Enable `phpThunder.diagnostics.enableVendor: true` for full analysis of third-party code.

## Rename Symbol (Pro)

`F2` on any symbol triggers a workspace-wide rename that updates every reference: the declaration, all usages, and any qualified references in other files.

<!-- MEDIA: screenshot of rename preview with changed files listed -->

> 📸 _Coming soon: screenshot of the rename preview dialog._

## Code generation (Pro)

PhpThunder can generate boilerplate:

- **Generate Getter / Setter** — creates accessor methods for properties, respecting the property type and PHPDoc
- **Generate missing accessors** — scans a class and offers to fill in any getters or setters that don't exist yet
- **Implement Missing Methods** — when a class declares an interface or extends an abstract class, PhpThunder generates stubs for all required methods

These are available as quick fixes (💡) directly on the class or property.

## Formatting

PhpThunder's formatter is configurable without being opinionated by default. Existing style can be preserved, or a specific layout can be enforced.

Configurable aspects include:

- **Arrays** — preserve as-is, auto-break on width, force single-line, or force multi-line
- **Parameters and arguments** — same four options for function/method definitions and call sites
- **Match arms** — formatting for `match` expressions
- **Control structures** — `if`, `foreach`, `for`, `while`, `switch` — choose between brace-style or alternative syntax
- **Max inline width** — the threshold at which `auto` mode breaks a single-line construct into multiple lines (default: 80)

All formatting settings live under `phpThunder.formatting.*`. See [Project configuration](07-project-configuration.md#formatting) for the full list.

### EditorConfig

PhpThunder's formatter also reads and applies .editorconfig files. The language server walks upward from the file's directory collecting `.editorconfig` files (stopping at the first file with `root = true`) and merges the resulting values with VS Code's formatting options before formatting.

Supported EditorConfig properties (recognized and applied):

- `indent_style` — "tab" or "space", sets whether the formatter uses tabs or spaces.
- `indent_size` — numeric or "tab", sets the indent size (when "tab" the `tab_width` is used if present).
- `tab_width` — numeric, controls how many spaces a tab represents and may influence `indent_size`.
- `end_of_line` — "lf" or "crlf", controls the line-ending sequence used when reformatting.
- `insert_final_newline` — `true`/`false`, whether a final newline is ensured at EOF.
- `trim_trailing_whitespace` — `true`/`false`, whether trailing whitespace is removed on formatted lines.

The server supports the usual EditorConfig glob patterns (wildcards `*` and `**`, `?`, character classes `[...]`, and alternation `{a,b}`), and anchored patterns starting with `/` are honored. Parsed .editorconfig files are cached by the server and invalidated when the file size or modification time changes.

Where this is implemented:

- Server-side parsing and merge: [pkg/formatter/editorconfig.go](pkg/formatter/editorconfig.go)
- Formatting invocation and options merge: [pkg/lsp/handlers_formatting.go](pkg/lsp/handlers_formatting.go#L20-L40)
- VS Code provider that delegates formatting to the server: [extension/src/formattingProviders.ts](extension/src/formattingProviders.ts)

When both VS Code/editor settings and `.editorconfig` provide values, the server starts from VS Code's `editor` formatting options and overrides only the fields explicitly set by `.editorconfig`.

## TODO workflows

The TODO panel scans the codebase for comment markers (`TODO`, `FIXME`, etc.) and surfaces them in one place.

Key commands:

- `PhpThunder: Focus TODOs` — open the TODO panel
- `PhpThunder: Refresh TODOs` — rescan after bulk changes
- `PhpThunder: Filter TODOs` — narrow down by keyword or file
- `PhpThunder: Group TODOs` — switch between grouping by file, type, or priority

This is especially handy in larger codebases where TODOs scatter across dozens of files.

## Composer helpers

PhpThunder wraps common Composer operations for running them without leaving the editor:

- `PhpThunder: Composer Install`
- `PhpThunder: Composer Update`
- `PhpThunder: Composer Require Package`
- `PhpThunder: Composer Dump Autoload`
- `PhpThunder: Composer Validate`

Output from Composer appears in the PhpThunder output channel, where the changes are visible.

## Next steps

- [Debugging](04-debugging.md) — set up Xdebug and start debugging
- [Project configuration](07-project-configuration.md) — all formatting, diagnostic, and code-fix settings
- [Free vs Pro](08-free-vs-pro.md) — full breakdown of which features require a Pro license
- [Troubleshooting](09-troubleshooting.md) — if the editor state doesn't match the project
