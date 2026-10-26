---
name: shell-review
description: Review a shell diff for quoting bugs, unsafe options, injection, and portability. Use on .sh patches and shell snippets after the script is written.
category: shell
tags: [review, shell, quoting]
---

# shell-review

Review the patch, not the idea of the patch. Quoting and failure handling first, then style.

## When to use

- A PR or local diff touches `.sh`, `.bash`, shell functions, or a `Makefile` recipe that embeds a multi-line script
- A script gained `eval`, `sh -c`, pipes to a shell, or unquoted expansions
- It is unclear whether the script is POSIX `sh` or bash

## When not to

- The task is to write a new script — use `shell-script`
- The diff is not shell
- The user asked for a feature, not a review

## Look at

1. **Options** — missing `set -euo pipefail` (bash) or `set -eu` (POSIX). `pipefail` used under `#!/bin/sh`. A later `set +e` that hides a real failure.
2. **Quoting** — unquoted `$var`, `$(...)`, or `$*`. `for f in $(ls …)`. Arrays expanded as `$array` instead of `"${array[@]}"`.
3. **Injection** — `eval`, `sh -c "$var"`, `bash -c` with concatenated input, `ssh host "$cmd"` built from untrusted strings, `xargs` without `-0` / `-d`.
4. **Word splitting and globs** — unquoted paths, `IFS` changes that are not restored, `*` or `?` in data that can expand to filenames.
5. **Conditionals** — `[ $a = $b ]` instead of `[ "$a" = "$b" ]`. `[[ ]]` or `(( ))` in a script whose shebang is `sh`. `==` inside `[`.
6. **Failures** — pipelines whose earlier command’s status is discarded. Commands whose non-zero exit is intentional but not marked (`|| true` with a comment). Missing non-zero exit when a required file or command is absent.
7. **Files and temp** — predictable `/tmp` names, no `mktemp`, no `EXIT` trap, redirects that clobber a real file (`>` instead of `>>`) without a reason.
8. **Portability** — bash-only syntax under `#!/bin/sh` (`[[ ]]`, arrays, `source` vs `.`, `${var,,}`, process substitution). GNU-only flags (`grep -P`, `sed -i` without a backup suffix argument) presented as portable.
9. **Secrets** — tokens, keys, or home paths echoed, written into the script, or left in `set -x` traces.

## Output

Write:

- **Summary** — what the shell change does
- **Blockers** — injection, unquoted expansions that split, wrong shell dialect, missing failure on error, temp-file races, leaked secrets
- **Notes** — naming, comments, redundant `cd`

Do not rewrite the script into another shell. Do not “fix” a failing command by dropping `set -e`.

## Done when

Blockers are empty or filed as required changes, and every finding names the line and the failure mode (split, inject, ignored status, or non-portable construct).
