# Profiling

Profiling is a Pro workflow in PhpThunder. It uses Xdebug profiling output and a built-in profiler panel so you can inspect slow requests without leaving VS Code.

## What profiling gives you

- profile capture for the currently active PHP file
- web profiling with a local PHP server
- a profiler panel that lists collected profiles and highlights hotspots
- persistent profile files in the workspace under `.phpthunder/profiles/`

## Requirements

You need:

- Pro access or an active trial
- a configured PHP interpreter
- Xdebug loaded for that interpreter

If Xdebug is missing, PhpThunder stops early and tells you which PHP binary failed the check.

## Profile the current file

Use `PhpThunder: Profile Current File` when you want a quick CLI-style profile for the file that is currently open in the editor.

Recommended flow:

1. Open the PHP file you want to measure.
2. Run `PhpThunder: Profile Current File`.
3. Let the script complete.
4. Review the generated profile in the profiler panel.

PhpThunder writes cachegrind files into `.phpthunder/profiles/` and opens the profiler panel so you can inspect the result.

## Start web profiling

Use `PhpThunder: Start Web Profiling` when you want to profile requests handled by a local PHP web server.

This flow is useful for:

- framework entry points
- controllers and routes that depend on HTTP context
- pages that are easier to inspect in a browser than from a single script run

The web profiling command:

- resolves the target workspace folder
- checks Xdebug on the selected interpreter
- starts a local PHP server using the configured doc root and port
- records cachegrind output under `.phpthunder/profiles/`
- opens the profiling UI

Use `PhpThunder: Stop Web Profiling Server` when you are done.

## Where profiles are stored

Profiles are written under:

```text
.phpthunder/profiles/cachegrind.out.*
```

PhpThunder also creates a `.gitignore` in that folder so profile artifacts are not accidentally committed.

## Relevant settings

The profiling workflow uses these settings:

- `phpThunder.profiling.webPort`
- `phpThunder.profiling.docRoot`

Example:

```json
{
  "phpThunder.profiling.webPort": 8000,
  "phpThunder.profiling.docRoot": "public"
}
```

## Profiler panel workflow

The profiler panel is the main review surface for collected profiles.

Use `PhpThunder: Open Profiler` to reopen it later and inspect existing captures. This is useful when:

- you already have saved cachegrind files
- you want to compare multiple recent runs
- you want to inspect hotspots after the original command finished

## Troubleshooting checklist

- Confirm the selected interpreter is the binary you actually use for the project.
- Confirm Xdebug is loaded for that binary.
- Confirm the profiling doc root exists in the workspace.
- Check whether another process is already using the preferred profiling port.
- Open the `PHP Profiler` output channel if you need extra detail.

## Next steps

- Continue with [Free vs Pro](08-free-vs-pro.md) if you need the current access boundary.
- Continue with [Troubleshooting](09-troubleshooting.md) if profiles are not generated or do not match the request you expected.
