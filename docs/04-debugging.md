# Debugging

PhpThunder includes a PHP debugger for VS Code that speaks to Xdebug and supports CLI, web, and attach workflows.

## Before you start

You need:

- a PHP interpreter configured for the workspace
- Xdebug installed and enabled for the interpreter you plan to use
- a reachable Xdebug port, usually `9003`

For launch configurations, the debug type is `phpThunder`.

## Debug modes

PhpThunder supports three common flows:

- `launch` with `mode: "cli"` for single-script debugging
- `launch` with `mode: "web"` for built-in web-server workflows
- `attach` to wait for an incoming Xdebug connection

## Example launch.json

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "phpThunder",
      "request": "launch",
      "name": "Launch PHP script",
      "program": "${file}",
      "cwd": "${workspaceFolder}",
      "port": 9003
    },
    {
      "type": "phpThunder",
      "request": "launch",
      "name": "PHP Web Server",
      "mode": "web",
      "cwd": "${workspaceFolder}",
      "port": 9003,
      "server": {
        "docRoot": "public",
        "webPort": 8000,
        "openBrowser": "ask"
      }
    },
    {
      "type": "phpThunder",
      "request": "attach",
      "name": "Attach to Xdebug",
      "hostname": "127.0.0.1",
      "port": 9003
    }
  ]
}
```

## Important launch fields

- `program`: PHP script to run in CLI mode
- `args`: command-line arguments for CLI mode
- `cwd`: working directory for the PHP process
- `env`: environment variables for the launched process
- `phpBin`: override the configured interpreter for a specific launch configuration
- `xdebugIniPath`: use a custom `php.ini` that loads Xdebug
- `generateIni`: let PhpThunder generate `.vscode/phpThunder.ini` if Xdebug is not already active
- `pathMappings`: remote-to-local mappings for Docker or remote hosts

## Web-mode fields

When `mode` is `web`, the nested `server` object can control the local HTTP server:

- `command`: override the auto-detected server command
- `docRoot`: document root relative to `cwd`
- `router`: router script relative to `cwd`
- `urlPath`: initial request path after the server starts
- `webPort`: preferred HTTP port
- `openBrowser`: `external`, `webview`, `ask`, or `false`

This is a good fit for small apps, built-in server workflows, or framework bootstraps where a local command can serve the project.

## Remote and container debugging

Use `attach` plus `pathMappings` when PHP runs somewhere other than the local workspace path.

Example:

```json
{
  "type": "phpThunder",
  "request": "attach",
  "name": "Attach to container Xdebug",
  "hostname": "127.0.0.1",
  "port": 9003,
  "pathMappings": {
    "/var/www/html": "${workspaceFolder}"
  }
}
```

## A simple debug routine

1. Confirm the selected interpreter is the one you actually use for the project.
2. Confirm Xdebug is loaded for that interpreter.
3. Start with a minimal `launch` or `attach` configuration.
4. Set one or two breakpoints.
5. Expand into path mappings or server overrides only if the simple setup is not enough.

## Next steps

- Continue with [Profiling](05-profiling.md) if you also want performance analysis.
- Continue with [Troubleshooting](09-troubleshooting.md) if breakpoints do not bind or connections never arrive.
