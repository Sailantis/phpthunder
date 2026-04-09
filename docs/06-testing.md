# Testing

PhpThunder integrates with the VS Code Test Explorer and can discover both PHPUnit and Pest tests.

## What PhpThunder discovers

PhpThunder organizes tests by file and then by test group:

- PHPUnit tests are grouped by class and method
- Pest tests are grouped by describe block when one exists
- data sets are shown as individual child items when the test framework exposes them

This makes the built-in VS Code Test Explorer useful even in mixed PHPUnit and Pest codebases.

## Running tests

Use the normal VS Code testing UI to run tests after PhpThunder has discovered them.

The extension can use:

- PHPUnit
- Pest
- automatic runner selection based on project contents

The runner is controlled by `phpThunder.testRunner`.

## Debugging tests

PhpThunder also provides a dedicated `Debug Tests` profile in the Test Explorer.

That flow uses:

- the active PhpThunder interpreter for the workspace
- the configured test runner
- the PhpThunder debugger

If debug test runs do not start, treat the problem like a normal Xdebug setup issue and review [Debugging](04-debugging.md).

## Recommended setting

```json
{
  "phpThunder.testRunner": "auto"
}
```

Available values:

- `auto`
- `phpunit`
- `pest`

`auto` prefers Pest when `vendor/bin/pest` exists and otherwise falls back to PHPUnit.

## Tips for reliable discovery

- Open the project root, not only a nested source folder.
- Make sure dependencies are installed if the test runner lives under `vendor/bin/`.
- Reindex the project after major structural changes.
- Keep the PHP version setting aligned with the project to reduce noisy diagnostics around tests.

## When tests do not appear

Check these first:

- `vendor/bin/phpunit` or `vendor/bin/pest` exists
- `phpThunder.testRunner` is set correctly
- the workspace folder is the project root
- the interpreter can actually execute the test binary

## Next steps

- Continue with [Project configuration](07-project-configuration.md) for runner and interpreter settings.
- Continue with [Troubleshooting](09-troubleshooting.md) if the Test Explorer remains empty.
