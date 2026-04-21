# Installation and activation

This guide covers the full setup path for PhpThunder: installing the extension, pointing it at the right PHP binary, tuning workspace settings, and activating a license when you're ready for Pro features.

## Install the extension

Install PhpThunder from the VS Code marketplace the same way you install any other extension. Once installed, open a folder that contains PHP files — the extension activates automatically and begins its initial project scan.

## Configure the PHP interpreter

PhpThunder uses a named interpreter catalog rather than a raw path. This makes it easy to switch between multiple PHP versions in different projects.

1. Run `PhpThunder: Configure PHP Interpreters`.
2. Add or auto-detect your PHP binaries. You can add as many as you need (PHP 8.1, 8.2, 8.3, etc.).
3. Choose which interpreter should be active for the current workspace.

> **Important:** `phpThunder.activeInterpreter` stores the interpreter _name_ from the PhpThunder catalog, not a file path. Make sure the name in your `settings.json` matches exactly what appears in the interpreter UI.

> **Tip:** Teams working across multiple projects with different PHP versions can add all of them to the catalog once and then select per workspace — no need to reconfigure global PATH every time.

## Select the PHP language level

Run `PhpThunder: Select PHP Version` and pick the language level that matches the current project. This drives diagnostics, type analysis, and feature-compatibility checks.

The underlying setting is `phpThunder.phpVersion`. You can set it per workspace folder in `.vscode/settings.json` so each project in a multi-root setup runs its own level.

## Configure Composer and include paths

PhpThunder exposes dedicated commands for project infrastructure:

- **`PhpThunder: Configure Composer`** — useful when the project ships its own `composer.phar` or uses a non-standard Composer binary location.
- **`PhpThunder: Configure Include Paths`** — use this when the project depends on PHP directories that live outside the standard Composer graph (legacy stubs, internal monorepo packages, etc.).

After changing include paths, run `PhpThunder: Reindex Project` or reload the VS Code window to pick up the changes.

## Activate a trial or Pro license

PhpThunder offers a full free tier, a 30-day Pro trial, and ongoing Pro access. When you're ready to unlock Pro features, run `PhpThunder: Activate License`.

From the activation page you can:

- **Sign in with your account** to fetch and activate a license associated with your email
- **Enter a license key directly** if you already have one

<!-- MEDIA: screenshot of the activation dialog -->

> 📸 _Coming soon: screenshot of the activation flow._

### Status bar states

The status bar entry tells you your current access level at a glance:

| Status bar shows   | What it means                                                       |
| ------------------ | ------------------------------------------------------------------- |
| `PHP Free`         | Base features only — no trial active                                |
| `PHP Trial`        | Full Pro access for the trial period                                |
| `PHP Pro`          | Active Pro license                                                  |
| `PHP Grace Period` | License recently expired; Pro features remain available temporarily |

> **Grace Period:** If your Pro license lapses, PhpThunder enters a Grace Period so you're not immediately blocked. You can reactivate or renew from `PhpThunder: Activate License` at any time. See the [FAQ](10-faq.md#what-is-the-grace-period) for more detail.

For pricing and plan details, see the [Sailantis website](https://sailantis.io).

## Suggested workspace settings

A good starting point for `.vscode/settings.json`:

```json
{
  "phpThunder.phpVersion": "8.3",
  "phpThunder.activeInterpreter": "PHP 8.3",
  "phpThunder.testRunner": "auto",
  "phpThunder.composer.mode": "auto",
  "phpThunder.includePaths": ["stubs", "packages/shared/src"]
}
```

Adjust the PHP version, interpreter name, and paths to match your project.

## Useful configuration commands

| Command                                  | Purpose                                       |
| ---------------------------------------- | --------------------------------------------- |
| `PhpThunder: Configure PHP Interpreters` | Add, remove, and select PHP binaries          |
| `PhpThunder: Select PHP Version`         | Set the language level for the current folder |
| `PhpThunder: Configure Composer`         | Customize Composer binary resolution          |
| `PhpThunder: Configure Include Paths`    | Add extra source directories to the index     |
| `PhpThunder: Activate License`           | Start a trial or activate a Pro license       |

## Next steps

- [Editor features](03-editor-features.md) — completion, diagnostics, formatting, and more
- [Project configuration](07-project-configuration.md) — full settings reference
- [Free vs Pro](08-free-vs-pro.md) — which workflows require Pro access
- [FAQ](10-faq.md) — common questions about activation and licensing
