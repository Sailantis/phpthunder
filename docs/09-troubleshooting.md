# Troubleshooting

This page covers the problems that most commonly block a smooth PhpThunder experience. Start with the Quick wins section — most issues are resolved in one step.

## Quick wins

If something feels off, try these first before digging deeper:

| Symptom                                 | Fix                                                                                            |
| --------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Completion or hover is missing          | Run `PhpThunder: Reindex Project`                                                              |
| Wrong diagnostics for language features | Run `PhpThunder: Select PHP Version` and set the correct level                                 |
| Vendor symbols are missing              | Run `composer install`, then `PhpThunder: Reindex Project`                                     |
| Tests don't appear in Test Explorer     | Confirm `vendor/bin/phpunit` or `vendor/bin/pest` exists and run `PhpThunder: Reindex Project` |

If a quick win doesn't solve it, find the relevant section below.

---

## PhpThunder doesn't see recent project changes

**Symptoms:** Completion is stale, recently added classes don't resolve, renamed files still show the old name.

**Fix:**

1. Save the affected files.
2. Run `PhpThunder: Reindex Project`.
3. Wait for the scan to complete — the status bar shows progress.

This is especially important after large refactors, Composer operations, or include-path changes. Most single-file edits are picked up automatically; reindex is for changes that affect the whole project graph.

---

## Vendor classes or Composer symbols are missing

**Symptoms:** Third-party classes show as undefined, completion doesn't include Composer dependencies, `use` statements can't be resolved.

**Fix:** Work through this checklist:

- Confirm `composer install` has been run and `vendor/` is populated.
- Confirm the workspace root is the project root (the folder containing `composer.json`), not a nested subfolder.
- Check that `phpThunder.includePaths` includes any non-standard source directories the project depends on.
- Run `PhpThunder: Composer Dump Autoload` or `PhpThunder: Reindex Project` after autoload changes.

> **Note:** `phpThunder.diagnostics.enableVendor` is off by default, so vendor files intentionally don't behave like first-party code unless you enable that setting.

---

## The wrong PHP version is used for analysis

**Symptoms:** False-positive diagnostics about features that actually exist in the project's PHP version, or missing diagnostics for features that aren't supported.

**Fix:** Run `PhpThunder: Select PHP Version` and choose the version the project actually targets.

This is the first setting to check when you see version-feature warnings that don't match reality.

---

## The wrong PHP binary is used

**Symptoms:** Debugging or tests use a different PHP version than expected, Composer commands fail, Xdebug checks fail for an interpreter that should have it.

**Fix:** Run `PhpThunder: Configure PHP Interpreters` and verify:

- The correct PHP binary is in the interpreter catalog.
- The intended interpreter is selected for the current workspace.
- The selected interpreter can actually execute project commands.

---

## Include-path changes don't take effect

**Symptoms:** Newly added include paths don't resolve symbols, extra directories aren't being analyzed.

**Fix:** After editing `phpThunder.includePaths`:

- Run `PhpThunder: Reindex Project`, **or**
- Reload the VS Code window (`Developer: Reload Window`)

Include-path changes affect the indexing graph and aren't picked up without a refresh.

---

## Debugging doesn't start or breakpoints don't bind

**Symptoms:** `F5` fails with a connection error, breakpoints show as unverified, execution runs to completion without pausing.

**Fix:** Check these points:

- Xdebug is installed and loaded for the selected PHP binary (`php -m | grep xdebug`).
- The debug port in `launch.json` matches your Xdebug configuration (usually `9003`).
- Enable `generateIni` in the launch config if you want PhpThunder to generate a helper ini file automatically.
- For Docker or remote paths, `pathMappings` keys are the _remote_ paths and values are the _local_ paths — getting this backwards is a common mistake.
- The launch mode (`cli`, `web`, or `attach`) matches the actual workflow.

Start with the simplest possible configuration and add server overrides or path mappings only when the basic setup works.

---

## Profiling doesn't produce a capture

**Symptoms:** No cachegrind file appears under `.phpthunder/profiles/`, the profiler panel is empty.

**Fix:** Check these points:

- You have Pro access or an active trial.
- Xdebug is loaded for the selected interpreter.
- `phpThunder.profiling.docRoot` exists in the workspace (for web profiling).
- No other process is using the configured web port.
- Check the `PHP Profiler` output channel for detailed error messages.

---

## Tests are not discovered

**Symptoms:** The Test Explorer shows no tests, or shows far fewer than expected.

**Fix:** Check these points:

- The project contains PHPUnit or Pest test files that follow the expected naming convention.
- `vendor/bin/phpunit` or `vendor/bin/pest` exists (run `composer install` first).
- `phpThunder.testRunner` matches the project's actual runner, or is set to `auto`.
- The workspace root is the project root, not a nested source folder.
- The configured PHP interpreter can execute the test binary.

---

## I need more detail for a bug report

The LSP trace log is the most useful artifact for diagnosing PhpThunder behavior.

**Steps:**

1. Set `phpThunder.trace.server` to `messages` or `verbose` in your workspace settings.
2. Reproduce the problem.
3. Open the `PhpThunder Language Server` output channel (`View → Output` → select from the dropdown).
4. Copy the relevant portion of the log.
5. Reset `phpThunder.trace.server` back to `off` when you're done.

**Useful context to include in a bug report:**

- VS Code version
- PhpThunder version
- PHP version and selected interpreter name
- Whether the project uses Composer, Pest, PHPUnit, Xdebug, or custom include paths
- The minimal code or project layout that reproduces the issue

---

## Related guides

- [Project configuration](07-project-configuration.md) — settings reference
- [Debugging](04-debugging.md) — Xdebug setup in detail
- [Profiling](05-profiling.md) — profiling requirements and settings
- [Testing](06-testing.md) — test discovery and runner setup
- [FAQ](10-faq.md) — common questions about features and licensing
