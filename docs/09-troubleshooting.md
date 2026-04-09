# Troubleshooting

This page focuses on the problems that are most likely to block adoption: stale project state, wrong interpreter settings, missing test or debug behavior, and poor visibility into what PhpThunder is doing.

## PhpThunder does not see recent project changes

Try this first:

1. Save the affected files.
2. Run `PhpThunder: Reindex Project`.
3. Wait for the project scan to finish.

This is especially important after large refactors, Composer changes, or include-path changes.

## Vendor classes or Composer symbols are missing

Check these points:

- Composer dependencies are actually installed.
- The workspace root is the project root that contains `composer.json`.
- `phpThunder.includePaths` includes any non-standard source directories the project depends on.
- You ran `PhpThunder: Composer Dump Autoload` or `PhpThunder: Reindex Project` after major autoload changes.

Remember that `phpThunder.diagnostics.enableVendor` is disabled by default, so vendor files are not meant to behave like first-party code unless you opt into that mode.

## The wrong PHP version is used for analysis

Set `phpThunder.phpVersion` for the current folder with `PhpThunder: Select PHP Version`.

If you see language-feature warnings that do not match the project, this is the first setting to verify.

## The wrong PHP binary is used

Open `PhpThunder: Configure PHP Interpreters` and confirm that:

- the correct PHP binary is present in the interpreter catalog
- the intended interpreter is selected for the workspace
- the selected interpreter can actually execute your project commands

## Include-path changes do not take effect

After editing `phpThunder.includePaths`:

- run `PhpThunder: Reindex Project`, or
- reload the VS Code window

Include-path changes affect indexing and are not something you should expect to appear instantly without a refresh.

## Debugging does not start or breakpoints do not bind

Check these points:

- Xdebug is installed and loaded for the selected PHP binary.
- The configured debug port matches your Xdebug setup, usually `9003`.
- `generateIni` is enabled if you want PhpThunder to generate a helper ini file.
- `pathMappings` are set correctly for Docker or remote paths.
- The chosen launch mode matches the real workflow: CLI, web, or attach.

Use the minimal configuration first, then add custom server commands or path mappings only when needed.

## Profiling does not produce a capture

Check these points:

- the workflow is running with Pro access or an active trial
- Xdebug is loaded for the selected interpreter
- the profiling doc root exists when using web profiling
- another process is not already using the preferred web port
- the `PHP Profiler` output channel contains useful error details

## Tests are not discovered

Check these points:

- the project actually contains PHPUnit or Pest tests
- `vendor/bin/phpunit` or `vendor/bin/pest` exists
- `phpThunder.testRunner` is set correctly
- the workspace root is not too narrow
- the configured interpreter can run the selected test binary

## I need more detail for a bug report

Use these steps:

1. Set `phpThunder.trace.server` to `messages` or `verbose`.
2. Reproduce the problem.
3. Capture the relevant output and the minimal code sample.
4. Reset tracing back to `off` when you are done.

Useful context for a report:

- VS Code version
- PhpThunder version
- PHP version and selected interpreter
- whether the project uses Composer, Pest, PHPUnit, Xdebug, or custom include paths

## Related guides

- [Project configuration](07-project-configuration.md)
- [Debugging](04-debugging.md)
- [Profiling](05-profiling.md)
- [Testing](06-testing.md)
