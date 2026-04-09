# Getting started

This guide gets a PHP workspace into a usable PhpThunder state as quickly as possible.

## What you need

- VS Code
- A workspace folder that contains PHP files
- A working PHP binary if you want debugging, tests, Composer commands, or profiling
- Xdebug if you plan to debug or profile
- Composer if your project depends on `vendor/` packages or autoloading

## First-run checklist

1. Install the PhpThunder extension in VS Code.
2. Open the PHP project folder.
3. Run `PhpThunder: Select PHP Version` and choose the language level your project targets.
4. Run `PhpThunder: Configure PHP Interpreters` if the default `php` on PATH is not the binary you want to use.
5. Open a PHP file and let the initial scan finish.
6. If you changed Composer configuration, include paths, or the workspace structure, run `PhpThunder: Reindex Project`.

## What you should see

- Completion for classes, functions, constants, and members
- Hover information for symbols and inferred types
- Diagnostics for syntax, type, and selected PHPDoc issues
- Import assistance and organize-import workflows
- Tests in the VS Code Test Explorer when the project contains PHPUnit or Pest tests
- A status-bar state that reflects Free, Trial, or Pro access

## Commands worth memorizing

- `PhpThunder: Select PHP Version`
- `PhpThunder: Configure PHP Interpreters`
- `PhpThunder: Reindex Project`
- `PhpThunder: Configure Composer`
- `PhpThunder: Configure Include Paths`
- `PhpThunder: Activate License`

## Good first tasks

1. Open a model or controller and verify completion, hover, and diagnostics.
2. Format a file and see whether the default formatting mode matches the project style.
3. Open the Test Explorer if the project uses PHPUnit or Pest.
4. Create a basic `launch.json` entry if you expect to debug often.

## When to reindex

Run `PhpThunder: Reindex Project` after:

- major Composer changes
- changing `phpThunder.includePaths`
- switching PHP version assumptions for the folder
- moving or renaming many files outside the editor

## Next steps

- Continue with [Installation and activation](02-installation-and-activation.md) if you still need to configure the workspace.
- Continue with [Editor features](03-editor-features.md) for daily editing workflows.
- Continue with [Debugging](04-debugging.md) if your next goal is Xdebug.
