---
name: python-review
description: Review a Python diff for bugs, API misuse, missing tests, and dependency changes. Use on Python patches after the code is written.
category: python
tags: [review, python, testing]
---

# python-review

Review the patch, not the idea of the patch. Correctness first, then structure.

## When to use

- A PR or local diff touches `.py`, `pyproject.toml`, `requirements*.txt`, `setup.cfg`, or `tox.ini`
- Behavior changed and it is unclear whether tests cover it
- A new dependency, entry point, or public function was added

## When not to

- The task is only to run the suite — use `pytest`
- The diff is not Python
- The user asked for a feature, not a review

## Look at

1. **Behavior** — wrong return values, swallowed exceptions (`except Exception: pass`), bare `except:`, mutable default arguments, `is` used for equality.
2. **Types and contracts** — public functions whose inputs/outputs changed without callers or stubs updated; `Optional` values used without a check.
3. **Resources** — files, sockets, locks, and subprocesses opened without a context manager or an explicit close on every path.
4. **Concurrency** — shared mutable state, blocking calls inside async functions, tasks created and never awaited.
5. **Security** — `eval` / `exec` / `pickle` on untrusted input, `shell=True` with interpolated strings, secrets written into logs or tracked files.
6. **Packaging** — new imports with no dependency entry; version pins changed without a reason; packages imported that the project does not declare.
7. **Tests** — new branches and bug fixes with no test; tests that assert on mock internals instead of the result.

## Output

Write:

- **Summary** — what the Python change does
- **Blockers** — incorrect behavior, resource leaks, security issues, missing dependency declarations
- **Notes** — naming, typing, test gaps that are not blockers

Do not restyle the whole file. Do not replace the project’s formatter or type checker with a different one.

## Done when

Blockers are empty or each one names a file and the failing behavior, and notes do not duplicate blockers.
