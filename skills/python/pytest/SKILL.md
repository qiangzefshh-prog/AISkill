---
name: pytest
description: Run and write pytest tests using the project’s existing config. Use when adding coverage or checking a Python change.
category: python
tags: [pytest, testing, python]
---

# pytest

Use the repo’s test runner and layout. Do not invent a second way to run tests.

## When to use

- A Python change needs a regression test or new coverage
- Tests should be run after an edit
- A failure needs to be narrowed to one test or file

## When not to

- The project does not use pytest (it uses `unittest` invocation, `nose`, or a custom runner) — follow that runner
- The task is reviewing a diff rather than adding or running tests — use `python-review`
- The request is to weaken or delete a failing test to make the suite pass

## Steps

1. Find how this repo runs tests: `pyproject.toml` (`[tool.pytest.ini_options]`), `pytest.ini`, `tox.ini`, `noxfile.py`, or a documented script. Read it before adding flags or dependencies.
2. Run the narrowest useful set first:
   - one test: `pytest path/to/test_file.py::test_name`
   - one file: `pytest path/to/test_file.py`
   - the suite, only when the change is wide: the project’s documented command (often `pytest`)
3. Match existing style in the nearest test module: fixtures, `tmp_path`, parametrize, markers, and assertion helpers already in use. Do not add a new plugin unless the project already depends on it.
4. Test behavior through the public function or CLI, not private helpers. One failure mode per test. Name the test after the behavior (`test_<what>_<condition>`).
5. For a bug fix, add a test that fails before the fix and passes after. Do not assert on exact exception message text unless the message is part of the contract.
6. Keep tests free of network, real clocks, and machine paths unless the suite already provides fixtures for them. Use `tmp_path` for files.
7. If a test needs a marker (`slow`, `integration`), use one the config already defines. Do not skip a test to hide a failure.

## Done when

The new or changed tests pass under the project’s runner, fail for the reason they claim when the behavior is wrong, and do not require a new pytest plugin or a host-specific path.
