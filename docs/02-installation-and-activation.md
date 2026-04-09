# Installation and activation

This guide covers the initial setup path for PhpThunder: install the extension, point it at the right PHP binary, tune the project-level settings, and activate a trial or Pro license when needed.

## Install the extension

Install PhpThunder in VS Code the same way you install other extensions. After installation, open a workspace that contains PHP files so the extension can activate and scan the project.

## Configure the PHP interpreter

PhpThunder can work with the default `php` available on PATH, but most teams should explicitly select the binary they want to use.

1. Run `PhpThunder: Configure PHP Interpreters`.
2. Add or auto-detect PHP binaries.
3. Choose the interpreter that should be active for the current workspace.

Important detail: `phpThunder.activeInterpreter` stores the interpreter name from the PhpThunder catalog, not the raw path.

## Select the PHP language level

Run `PhpThunder: Select PHP Version` and choose the language level that matches the current folder. This affects diagnostics, feature checks, and analysis behavior.

The setting behind the command is `phpThunder.phpVersion`.

## Configure Composer and include paths

PhpThunder exposes dedicated setup commands for project infrastructure:

- `PhpThunder: Configure Composer`
- `PhpThunder: Configure Include Paths`

Use Composer configuration when the project needs a specific `composer.phar` or a custom Composer binary resolution strategy. Use include paths when the project depends on extra PHP directories outside the normal Composer graph.

After changing include paths, run `PhpThunder: Reindex Project` or reload the window.

## Activate a trial or Pro license

Run `PhpThunder: Activate License` to open the license page.

From there you can:

- sign in with email and password to fetch available licenses
- activate directly with a license key
- move from Free mode into Trial or Pro mode

The status bar reflects the current access state:

- `PHP Free`
- `PHP Trial`
- `PHP Pro`
- `PHP Grace Period`

## Suggested workspace settings

Use this as a starting point in `.vscode/settings.json`:

```json
{
  "phpThunder.phpVersion": "8.3",
  "phpThunder.activeInterpreter": "PHP 8.3",
  "phpThunder.testRunner": "auto",
  "phpThunder.composer.mode": "auto",
  "phpThunder.composer.projectPhar": "./tools/composer.phar",
  "phpThunder.includePaths": ["stubs", "packages/shared/src"]
}
```

Adjust the interpreter name and paths to match your workspace.

## Useful configuration commands

- `PhpThunder: Configure PHP Interpreters`
- `PhpThunder: Configure Composer`
- `PhpThunder: Configure Include Paths`
- `PhpThunder: Select PHP Version`
- `PhpThunder: Activate License`

## Next steps

- Continue with [Editor features](03-editor-features.md) for daily editing workflows.
- Continue with [Project configuration](07-project-configuration.md) for a broader settings reference.
- Continue with [Free vs Pro](08-free-vs-pro.md) if you need the current feature boundary.
