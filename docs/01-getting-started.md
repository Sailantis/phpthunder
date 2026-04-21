# Getting started

Welcome to PhpThunder — a PHP language server, debugger, and workflow extension for VS Code. Within a few minutes of setup you'll have smart completion, hover documentation, live diagnostics, and one-click debugging for any PHP project, whether it's a small script or a large Composer-managed application.

This guide walks you through the first-run setup from a fresh install to a fully working workspace.

## What you need

| Requirement  | Why you need it                                                 |
| ------------ | --------------------------------------------------------------- |
| VS Code      | The extension host                                              |
| A PHP binary | Required for debugging, tests, profiling, and Composer commands |
| Xdebug       | Required for debugging and profiling                            |
| Composer     | Required if your project uses `vendor/` packages or autoloading |

You don't need all of these on day one. Code intelligence, diagnostics, and formatting work as soon as the extension activates — even without a configured binary.

## First-run walkthrough

Follow these steps the first time you open a PHP project with PhpThunder:

1. **Install the extension** in VS Code from the marketplace.
2. **Open your project folder** — the one that contains your PHP files (and ideally `composer.json` at the root).
3. **Pick a language level** — run `PhpThunder: Select PHP Version` and choose the version your project targets. This drives diagnostics, type analysis, and feature checks. If you're unsure, pick the version that your hosting environment runs.
4. **Point at the right PHP binary** — run `PhpThunder: Configure PHP Interpreters` if the system `php` on PATH isn't the one you want. You can add multiple binaries here; PhpThunder stores them by name.
5. **Wait for the initial scan** — open a PHP file and give PhpThunder a moment to index the project. The status bar shows progress.
6. **Reindex if needed** — if you recently changed Composer configuration, include paths, or the workspace structure, run `PhpThunder: Reindex Project` to pick up those changes.

> **Tip:** After cloning a fresh project, run `composer install` first, then open the folder in VS Code and let PhpThunder index the freshly-populated `vendor/` directory. This gives you completion and hover for all dependencies from the start.

<!-- MEDIA: GIF showing completion and hover in a PHP file after first setup -->

> 📸 _Coming soon: a short GIF showing completion and hover in action on a real project._

## What you should see after setup

Once the initial index is complete, you should have:

- **Completion** for classes, functions, constants, members, and imported namespaces
- **Hover documentation** for symbols and inferred types, including PHPDoc from your dependencies
- **Diagnostics** for syntax errors, type mismatches, and selected PHPDoc issues — shown inline as you type
- **Import assistance** that suggests and inserts `use` statements for unresolved short names
- **Test Explorer entries** if the project has PHPUnit or Pest tests in the standard locations
- **A status-bar entry** showing your current access state (Free, Trial, or Pro)

If anything is missing, a quick `PhpThunder: Reindex Project` resolves most first-run surprises.

## Commands worth memorizing

- `PhpThunder: Select PHP Version` — sets the language level for the current folder
- `PhpThunder: Configure PHP Interpreters` — add and manage PHP binaries
- `PhpThunder: Reindex Project` — rebuild the project index after structural changes
- `PhpThunder: Configure Composer` — customize how PhpThunder finds and runs Composer
- `PhpThunder: Configure Include Paths` — add extra source directories outside Composer's graph
- `PhpThunder: Activate License` — start a trial or activate a Pro license

## Good first tasks

1. **Verify the basics** — open a model or controller, trigger completion with `Ctrl+Space`, and hover a class or method name.
2. **Check formatting** — format a file (`Shift+Alt+F`) and confirm the output matches the project's style. Adjust `phpThunder.formatting.*` settings if needed.
3. **Open the Test Explorer** — if the project uses PHPUnit or Pest, the sidebar should already show your test tree.
4. **Set up a debug launch** — create a minimal `launch.json` entry now so it's ready when you need it. See [Debugging](04-debugging.md) for a quick template.

## When to reindex

Run `PhpThunder: Reindex Project` after:

- running `composer install` or `composer update`
- adding or changing `phpThunder.includePaths`
- switching the PHP version setting for the folder
- moving or renaming a large number of files outside the editor

Most single-file changes are picked up automatically. Reindex is for changes that affect the whole project graph.

## Next steps

- [Installation and activation](02-installation-and-activation.md) — configure the workspace and activate a Pro license
- [Editor features](03-editor-features.md) — day-to-day editing workflows in detail
- [Debugging](04-debugging.md) — wire up Xdebug and start your first debug session
