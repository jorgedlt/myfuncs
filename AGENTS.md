# AGENTS.md - MyFunc Bash Utility Library

## Build/Lint/Test Commands
- **Syntax check**: `bash -n .myfuncs`
- **Lint**: `shellcheck .myfuncs` (install shellcheck first: `sudo apt install shellcheck`)
- **Run single function test**: Source and call directly, e.g., `source .myfuncs && yqls`
- **Dependency check**: `source .myfuncs` (functions check dependencies at runtime)

## Code Style Guidelines

### Naming Conventions
- Functions: lowercase with underscores (`snake_case`) - `yqls`, `jqcheck`, `gitdiff`
- Variables: lowercase with underscores - `local input`, `local f`
- Constants: UPPERCASE with underscores - `CONFIG_YAML`, `COPY_COMMAND`

### Imports and Dependencies
- Check dependencies with `command -v tool >/dev/null 2>&1`
- Provide fallback behavior when dependencies missing
- Warn user via stderr when tools unavailable

### Error Handling
- Use `return 1` for errors, `return 0` for success
- Print error messages to stderr (`1>&2`)
- Validate inputs and show usage messages
- Graceful degradation when tools unavailable

### Formatting
- 2-space indentation
- Functions separated by comment headers with dashes
- Local variables declared at function start
- Command substitution: `$(command)` not backticks
- Conditional checks: `[ -z "$var" ]` for string checks

### Types and Variables
- Use `local` for function-scoped variables
- Quote variables: `"$var"` to prevent word splitting
- Default values: `${var:-default}`

### Comments and Documentation
- Section headers: `# ---` with descriptive titles
- Brief function comments above definitions
- No inline comments unless complex logic