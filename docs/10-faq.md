# FAQ

Answers to the questions that come up most often. If you're looking for a step-by-step guide, the links at the bottom of each section point you to the right place.

For pricing, plan details, and commercial questions, visit [sailantis.io](https://sailantis.io).

---

## Activation & licensing

### How do I activate Pro?

Run `PhpThunder: Activate License` from the VS Code command palette. The activation page lets you:

- Sign in with your Sailantis account to fetch available licenses
- Enter a license key directly if you already have one

The status bar updates immediately to reflect your new access level.

### How do I start a free trial?

PhpThunder offers a 30-day Pro trial — full access to every Pro feature, no credit card required. Run `PhpThunder: Activate License` and follow the trial option on the activation page.

### What happens when my trial ends?

When the trial period ends, the extension returns to Free mode. You keep all the Free features, and nothing breaks — you just lose access to the Pro-only workflows (Rename Symbol, code generation, profiling, inline debug values). You can activate a Pro license at any time from `PhpThunder: Activate License`.

### What is the Grace Period?

If a Pro license lapses (for example, a subscription renewal fails), PhpThunder enters a Grace Period instead of immediately cutting off Pro access. During the Grace Period, all Pro features remain available while you sort out the renewal. The status bar shows `PHP Grace Period` to remind you that action is needed.

Renew or reactivate from `PhpThunder: Activate License`.

### Can I use PhpThunder on multiple machines?

This depends on your license plan. See the [Sailantis website](https://sailantis.io) for current seat and machine limits.

### How do I move my license to a new machine?

Licenses are tied to your Sailantis account, not a specific machine. Sign in with `PhpThunder: Activate License` on the new machine and your license will activate there. If you run into machine-limit issues, check your license details on [sailantis.io](https://sailantis.io).

### I lost my license key. What do I do?

Log in to your account at [sailantis.io](https://sailantis.io) to retrieve your license key. You can also activate directly by signing in — no key needed if you use account-based activation.

---

## Free vs Pro

### What exactly does Pro unlock?

| Feature                    | What you can do                                                                  |
| -------------------------- | -------------------------------------------------------------------------------- |
| Rename Symbol              | Safely rename any class, method, function, or variable across the entire project |
| Generate Getter / Setter   | Create typed accessor methods without writing boilerplate                        |
| Generate missing accessors | Scan a class and fill in all missing getters and setters at once                 |
| Implement Missing Methods  | Generate stubs for all required abstract and interface methods                   |
| Pro code fixes (CF)        | Extra quick fixes for code-quality patterns                                      |
| Profile Current File       | Capture a Xdebug profile for the active PHP script in one command                |
| Start Web Profiling        | Profile HTTP requests via a local PHP server                                     |
| Open Profiler              | Review and compare captured profiles in a built-in panel                         |
| Inline debug values        | See variable values directly in the editor while paused in a debug session       |
| Starred completion         | Best completion candidates are pre-selected and starred                          |

Everything else — completion, hover, diagnostics, formatting, debugging, testing, Composer tools — is included in Free.

### Can I try Pro features before buying?

Yes. The 30-day Pro trial gives you full access to every Pro feature. Start it from `PhpThunder: Activate License`.

### Do I need a Pro license for basic debugging?

No. Xdebug-based debugging (CLI launch, web server launch, and attach) is fully included in Free. The only debugging feature that requires Pro is **inline debug values** — variable values shown directly in the editor while paused.

---

## Compatibility

### Which PHP versions are supported?

PhpThunder supports PHP 5.6 through 8.5. Set the language level per workspace with `PhpThunder: Select PHP Version`. Diagnostics, feature checks, and type analysis all respect the selected version.

### Which operating systems does PhpThunder support?

PhpThunder ships platform-specific binaries for:

- Windows (x64, ARM64)
- macOS (x64, ARM64)
- Linux (x64, ARM64)

### What is the minimum VS Code version?

VS Code 1.82.0 or later.

### Does PhpThunder work in WSL?

Yes. Open the folder in WSL via the Remote – WSL extension. PhpThunder activates normally; configure the PHP interpreter to a WSL-side binary using `PhpThunder: Configure PHP Interpreters`.

### Does it work with Dev Containers or remote SSH?

Yes. The extension runs on the remote host when you use the Remote – Containers or Remote – SSH extension. Configure the interpreter to the PHP binary available in that environment.

### Does PhpThunder work in a multi-root workspace?

Yes. PHP version and interpreter settings are per-folder, so each workspace root can target a different PHP version and binary independently.

---

## Common quick fixes

### Completion is missing for my classes

Run `PhpThunder: Reindex Project`. If symbols from `vendor/` are missing, make sure `composer install` has been run and the workspace root is the folder containing `composer.json`. See [Troubleshooting](09-troubleshooting.md#vendor-classes-or-composer-symbols-are-missing).

### I'm getting diagnostics for the wrong PHP version

Run `PhpThunder: Select PHP Version` and pick the version your project targets. See [Troubleshooting](09-troubleshooting.md#the-wrong-php-version-is-used-for-analysis).

### Debugging isn't connecting

Confirm Xdebug is loaded for the selected interpreter (`php -m | grep xdebug`) and that the port in `launch.json` matches your Xdebug config (usually `9003`). See [Debugging](04-debugging.md) and [Troubleshooting](09-troubleshooting.md#debugging-doesnt-start-or-breakpoints-dont-bind).

### My tests don't appear in the Test Explorer

Make sure `composer install` has been run so `vendor/bin/phpunit` or `vendor/bin/pest` exists, then run `PhpThunder: Reindex Project`. See [Testing](06-testing.md) and [Troubleshooting](09-troubleshooting.md#tests-are-not-discovered).

### PhpThunder seems slow or uses a lot of memory

Try disabling `phpThunder.diagnostics.enableVendor` if it's enabled — this can significantly reduce analysis load on large projects. For persistent performance issues, open a trace log (`phpThunder.trace.server: "messages"`) and check the `PhpThunder Language Server` output channel for clues.

---

## More questions

For **pricing, plan comparison, seat limits, renewals, and billing**, see the [Sailantis website](https://sailantis.com).

For **bug reports or feature requests**, use the issue tracker linked from the extension's marketplace page.

For **setup and configuration help**, start with [Getting started](01-getting-started.md) or [Troubleshooting](09-troubleshooting.md).

<!-- MEDIA: short video walkthrough of the activation flow -->

> 📸 _Coming soon: a short walkthrough video showing the activation flow from Free to Pro._
