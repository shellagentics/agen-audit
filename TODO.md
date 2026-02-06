# TODO: Rename `agen-audit` → `aaud`

This repo is being renamed from `agen-audit` to `aaud` as part of a toolkit-wide rename.
The GitHub repo will move from `shellagentics/agen-audit` to `shellagentics/aaud`.

## Summary of changes

| What | Old | New |
|------|-----|-----|
| Repo name | `agen-audit` | `aaud` |
| Executable | `agen-audit` | `aaud` |
| GitHub URL | `shellagentics/agen-audit` | `shellagentics/aaud` |

Note: `agen-audit` reads from `AGEN_LOG_DIR` which becomes `AGENT_LOG_DIR`.

Related renames (update cross-references):

| Old | New |
|-----|-----|
| `agen` (core tool) | `agent` |
| `agen-memory` | `amem` |
| `agen-log` | `alog` |
| `agen-skills` | `ascr` |
| `AGEN_LOG_DIR` | `AGENT_LOG_DIR` |

---

## File-by-file instructions

### 1. Rename the executable: `agen-audit` → `aaud`

```bash
mv agen-audit aaud
```

### 2. Edit `aaud` (the renamed executable)

This is the main script (~317 lines). Make these changes:

- **Header comment block**: Replace all `agen-audit` with `aaud`
- **die() prefix**: `"agen-audit: $*"` → `"aaud: $*"`
- **show_help()**: Update all text:
  - Tool name: `agen-audit` → `aaud`
  - Usage lines: `agen-audit --today` → `aaud --today` etc.
  - All example invocations
- **show_version()**: `"agen-audit $VERSION"` → `"aaud $VERSION"`
- **AGEN_LOG_DIR**: Replace all occurrences with `AGENT_LOG_DIR`
  - The default: `LOG_DIR="${AGEN_LOG_DIR:-./logs}"` → `LOG_DIR="${AGENT_LOG_DIR:-./logs}"`
  - Help text references
- **All comments** referencing `agen-audit` → `aaud`
- **References to `agen-log`**: Update to `alog` in comments/help

**Exact string replacements:**
- `agen-audit:` → `aaud:` (error messages)
- `agen-audit` → `aaud` (command name in help, comments, examples)
- `agen-log` → `alog` (cross-references)
- `AGEN_LOG_DIR` → `AGENT_LOG_DIR`

### 3. Edit `README.md`

Replace throughout:
- `# agen-audit` → `# aaud`
- All occurrences of `` `agen-audit` `` → `` `aaud` ``
- All code examples: `agen-audit --today` → `aaud --today` etc.
- `AGEN_LOG_DIR` → `AGENT_LOG_DIR`
- **NAME section**: `**agen-audit**` → `**aaud**`
- **SYNOPSIS**: Update all command examples
- **OPTIONS**: Update `--log-dir` default description
- **ENVIRONMENT section**: `AGEN_LOG_DIR` → `AGENT_LOG_DIR`
- **EXAMPLES section**: Update all invocations
- **SEE ALSO section**: Update cross-references:
  - `` `agen-log`(1) `` → `` `alog`(1) ``
  - `` `agen-memory`(1) `` → `` `amem`(1) ``
  - `` `agen`(1) `` → `` `agent`(1) ``
- **Comparison table** ("When to use agen-audit vs raw tools"): Update tool names
- **GitHub URLs**: Update if present
- **Shell Agentics section**: Update toolkit description
- **"What Is This?" section**: Update references to `agen-log` → `alog`

---

## Verification

After all changes, run:

```bash
# Ensure no stale references remain
grep -rn "agen-audit" .
grep -rn "agen-log" .
grep -rn "AGEN_" .

# Test help output
./aaud --help
./aaud --version
```

## Delete this file when done

Remove this TODO.md after completing all changes.
