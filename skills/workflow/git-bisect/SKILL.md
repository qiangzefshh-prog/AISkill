---
name: git-bisect
description: Find the commit that introduced a bug using automated or manual binary search. Use when isolating regression causes in git history.
category: workflow
tags: [git, bisect, debug]
---

# git-bisect

Pinpoint the exact commit that introduced a regression bug without guessing.

## When to use

- A test or build passes on an older commit but fails on HEAD
- A regression was reported and manual diff inspection is too slow or ambiguous
- A reproduction command or script exists that exits 0 on success and non-zero on failure

## When not to

- The defect has always existed (no known good commit)
- The repo history is linear and short enough to review in a single diff
- Flaky tests where runs produce inconsistent exit codes

## Steps

1. **Find boundary commits**: Identify a known bad commit (usually `HEAD`) and a known good commit (e.g. a previous release tag or hash).
2. **Formulate the test check**: Create a single non-interactive command or script (e.g., `npm test`, `pytest tests/test_regression.py`, `make test`).
3. **Start the bisect session**:
   ```bash
   git bisect start
   git bisect bad <bad-rev>
   git bisect good <good-rev>
   ```
4. **Run automated bisect** (recommended):
   ```bash
   git bisect run <repro-command-or-script>
   ```
   If manual testing is required, test each checked-out revision and mark with `git bisect good` or `git bisect bad`.
5. **Inspect the culprit**: Git outputs `<hash> is the first bad commit`. Inspect `git show <hash>` to understand the root cause.
6. **Reset the tree**: Always run `git bisect reset` to return HEAD to the original branch and clean up bisect state.

## Tips

- If a commit in the middle cannot be tested (e.g. broken build due to unrelated issue), run `git bisect skip` to test an adjacent commit.
- Exit code 125 tells `git bisect run` to skip the current commit.
- Ensure the test script does not leave untracked modified files that break subsequent checkouts.

## Done when

The culprit commit is identified, analyzed, and `git bisect reset` has restored the working branch.
