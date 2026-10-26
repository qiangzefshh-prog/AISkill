---
name: shell-script
description: Write a portable POSIX or bash script with safe options, quoting, and explicit exits. Use when adding or editing a .sh file or a shell entry point.
category: shell
tags: [shell, bash, posix]
---

# shell-script

Write a script the way the target shell actually runs it. Do not invent a second dialect in the same file.

## When to use

- Adding or editing a `.sh` script, a shell function library, or a `#!/bin/sh` / `#!/usr/bin/env bash` entry point
- A command sequence is being turned into a reusable script
- A script must run under `sh` on more than one Unix, or under bash on purpose

## When not to

- The file is a review of an existing script with no edits — use `shell-review`
- The task is a one-off command in an interactive shell
- The project already has a task runner (`make`, `just`, `npm`) that owns this step — extend that, do not add a parallel script

## Steps

1. Pick one shell and state it in the shebang. Use `#!/bin/sh` only for POSIX. Use `#!/usr/bin/env bash` when the script needs arrays, `[[ ]]`, or other bash features. Do not mix them.
2. For bash, start with `set -euo pipefail`. For POSIX `sh`, start with `set -eu`. Add `set -o pipefail` only when the shebang is bash (or another shell that documents it).
3. Quote every expansion that is data: `"$var"`, `"${var}"`, `"$@"`. Leave `$@` unquoted only when word-splitting is the intended interface, and say so in a comment. Do not use `eval` on constructed strings.
4. Name scratch files with `mktemp`. Remove them in a trap (`trap 'rm -f "$tmp"' EXIT`). Do not hard-code `/tmp/foo` or a home directory.
5. Check required commands with `command -v` before use. Exit non-zero with a short message on stderr (`echo "name: reason" >&2`) when a precondition fails.
6. Pass arguments as separate words. Never build a command line by concatenating untrusted input into `sh -c` or `bash -c`.
7. Make paths relative to the script or an explicit argument (`cd "$(dirname -- "$0")"` only when the script’s own directory is the contract). Do not embed a machine path.
8. Run the script with `sh -n` (or `bash -n`) and once with an empty environment for the variables it claims to require.

## Example

```sh
#!/bin/sh
set -eu

if ! command -v grep >/dev/null 2>&1; then
  echo "search: grep is required" >&2
  exit 1
fi

pattern=${1:?usage: search PATTERN FILE}
file=${2:?usage: search PATTERN FILE}
grep -F -e "$pattern" -- "$file"
```

## Done when

The script has one shebang, fails on unset variables and failed commands, quotes expansions, cleans up temp files, and passes a syntax check in the shell named by the shebang.
