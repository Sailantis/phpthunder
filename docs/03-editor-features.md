# Editor features

PhpThunder is first and foremost an editing toolchain. This page covers the workflows that make a real difference during everyday PHP development — from the moment you start typing to the moment you commit.

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

PhpThunder provides the core IDE behaviors you'd expect in a well-equipped PHP workspace.

### Completion

As you type, PhpThunder suggests global symbols (classes, functions, constants), class members, static access, and namespaced identifiers. The suggestions include method signatures, property types, and PHPDoc summaries so you don't need to jump to the definition just to check a parameter name.

> **Example:** Start typing `new Http` in a Laravel project and PhpThunder completes to `Illuminate\Http\Request`, adding the `use` statement at the top of the file if it's not already there.

<!-- MEDIA: GIF of completion with auto-import in a controller -->

> 📸 _Coming soon: GIF of completion and auto-import in a real controller._

### Hover

Hover over any symbol to see its type signature, return type, parameters, and PHPDoc — including documentation from Composer dependencies. No need to leave the file you're working on.

<!-- MEDIA: screenshot of hover showing type + PHPDoc -->

> 📸 _Coming soon: screenshot of hover documentation on a method._

### Go to definition and find references

`F12` jumps to the definition of any symbol. `Shift+F12` (or right-click → Find All References) shows everywhere a symbol is used, across the entire project including `vendor/` when you've opted into vendor analysis.

### Import assistance

When you use a short class name that PhpThunder can't resolve, it offers to add the missing `use` statement. When there are multiple candidates (e.g., both `App\Request` and `Illuminate\Http\Request`), it shows a picker.

> **Tip:** `PhpThunder: Organize Imports` removes unused `use` statements and sorts the remaining ones. Bind it to a key or run it as a source action on save.

## Diagnostics and quick fixes

PhpThunder publishes diagnostics for:

- **Parse and syntax problems** — caught as you type, no save needed
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

> **Note:** Vendor file diagnostics are off by default to keep the noise level low. Turn them on with `phpThunder.diagnostics.enableVendor: true` if you want full analysis of third-party code.

## Rename Symbol (Pro)

`F2` on any symbol triggers a workspace-wide rename that updates every reference: the declaration, all usages, and any qualified references in other files.

<!-- MEDIA: screenshot of rename preview with changed files listed -->

> 📸 _Coming soon: screenshot of the rename preview dialog._

## Code generation (Pro)

PhpThunder can generate boilerplate so you don't have to:

- **Generate Getter / Setter** — creates accessor methods for properties, respecting the property type and PHPDoc
- **Generate missing accessors** — scans a class and offers to fill in any getters or setters that don't exist yet
- **Implement Missing Methods** — when a class declares an interface or extends an abstract class, PhpThunder generates stubs for all required methods

These are available as quick fixes (💡) directly on the class or property.

## Formatting

PhpThunder's formatter is configurable without being opinionated by default. It can preserve your existing style or enforce a specific layout — your call.

Configurable aspects include:

- **Arrays** — preserve as-is, auto-break on width, force single-line, or force multi-line
- **Parameters and arguments** — same four options for function/method definitions and call sites
- **Match arms** — formatting for `match` expressions
- **Control structures** — `if`, `foreach`, `for`, `while`, `switch` — choose between brace-style or alternative syntax
- **Max inline width** — the threshold at which `auto` mode breaks a single-line construct into multiple lines (default: 80)

All formatting settings live under `phpThunder.formatting.*`. See [Project configuration](07-project-configuration.md#formatting) for the full list.

## TODO workflows

The TODO panel scans your codebase for comment markers (`TODO`, `FIXME`, etc.) and surfaces them in one place.

Key commands:

- `PhpThunder: Focus TODOs` — open the TODO panel
- `PhpThunder: Refresh TODOs` — rescan after bulk changes
- `PhpThunder: Filter TODOs` — narrow down by keyword or file
- `PhpThunder: Group TODOs` — switch between grouping by file, type, or priority

This is especially handy in larger codebases where TODOs scatter across dozens of files.

## Composer helpers

PhpThunder wraps common Composer operations so you can run them without leaving the editor:

- `PhpThunder: Composer Install`
- `PhpThunder: Composer Update`
- `PhpThunder: Composer Require Package`
- `PhpThunder: Composer Dump Autoload`
- `PhpThunder: Composer Validate`

Output from Composer appears in the PhpThunder output channel so you can see what changed.

## Next steps

- [Debugging](04-debugging.md) — set up Xdebug and start your first debug session
- [Project configuration](07-project-configuration.md) — all formatting, diagnostic, and code-fix settings
- [Free vs Pro](08-free-vs-pro.md) — full breakdown of which features require a Pro license
- [Troubleshooting](09-troubleshooting.md) — if the editor state doesn't match the project
