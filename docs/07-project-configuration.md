# Project configuration

This page collects the settings and commands that shape how PhpThunder behaves inside a workspace.

## Core workspace settings

### PHP version and interpreter

- `phpThunder.phpVersion`: language level for the current folder
- `phpThunder.activeInterpreter`: selected interpreter name for the workspace
- `phpThunder.interpreters`: machine-scoped interpreter catalog managed by the PhpThunder settings UI

Use these commands to configure them:

- `PhpThunder: Select PHP Version`
- `PhpThunder: Configure PHP Interpreters`

## Test runner

- `phpThunder.testRunner`: `auto`, `phpunit`, or `pest`

Use `auto` unless the workspace needs a fixed runner.

## Composer and include paths

- `phpThunder.composer.mode`: `auto`, `projectPhar`, or `custom`
- `phpThunder.composer.projectPhar`: project-relative path to a `composer.phar`
- `phpThunder.includePaths`: extra PHP directories to index

Useful commands:

- `PhpThunder: Configure Composer`
- `PhpThunder: Configure Include Paths`
- `PhpThunder: Composer Install`
- `PhpThunder: Composer Update`
- `PhpThunder: Composer Require Package`
- `PhpThunder: Composer Dump Autoload`
- `PhpThunder: Composer Validate`

After changing include paths, run `PhpThunder: Reindex Project` or reload the window.

## Diagnostics and code fixes

- `phpThunder.diagnostics.enableVendor`: enable diagnostics for files under `vendor/`
- `phpThunder.codeFixes.enabled`: toggle code-fix suggestions
- `phpThunder.codeFixes.disabledFixes`: disable individual fix IDs such as `CF001`

The default vendor behavior is intentionally conservative to avoid noisy third-party diagnostics.

## Formatting

Layout settings with the values `preserve`, `auto`, `force-single-line`, or `force-multi-line`:

- `phpThunder.formatting.arrays`
- `phpThunder.formatting.parameters`
- `phpThunder.formatting.arguments`
- `phpThunder.formatting.matchArms`

Syntax settings with the values `preserve`, `force-braces`, or `force-alternative`:

- `phpThunder.formatting.ifSyntax`
- `phpThunder.formatting.foreachSyntax`
- `phpThunder.formatting.forSyntax`
- `phpThunder.formatting.whileSyntax`
- `phpThunder.formatting.switchSyntax`

Width control:

- `phpThunder.formatting.maxInlineWidth`

## Profiling and tracing

- `phpThunder.profiling.webPort`
- `phpThunder.profiling.docRoot`
- `phpThunder.trace.server`

`phpThunder.trace.server` accepts `off`, `messages`, or `verbose`. Use `verbose` only when diagnosing extension behavior because it produces more log traffic.

## Example settings.json

```json
{
  "phpThunder.phpVersion": "8.3",
  "phpThunder.activeInterpreter": "PHP 8.3",
  "phpThunder.testRunner": "auto",
  "phpThunder.composer.mode": "auto",
  "phpThunder.composer.projectPhar": "./tools/composer.phar",
  "phpThunder.includePaths": ["stubs", "packages/shared/src"],
  "phpThunder.codeFixes.enabled": true,
  "phpThunder.diagnostics.enableVendor": false,
  "phpThunder.formatting.arrays": "preserve",
  "phpThunder.formatting.parameters": "auto",
  "phpThunder.formatting.arguments": "auto",
  "phpThunder.formatting.ifSyntax": "preserve",
  "phpThunder.formatting.maxInlineWidth": 100,
  "phpThunder.trace.server": "off"
}
```

## Operational commands

The commands you will use most often after configuration changes are:

- `PhpThunder: Reindex Project`
- `PhpThunder: Configure PHP Interpreters`
- `PhpThunder: Configure Composer`
- `PhpThunder: Configure Include Paths`
- `PhpThunder: Select PHP Version`

## Next steps

- Continue with [Free vs Pro](08-free-vs-pro.md) if you need to know which workflows depend on a license.
- Continue with [Troubleshooting](09-troubleshooting.md) if the project still behaves differently than expected after configuration changes.
