---
name: open-pr
description: Push the current branch and open a pull request against the default base. Use when commits are ready and a PR should be created or updated.
category: workflow
tags: [github, pull-request, git]
---

# open-pr

Open one pull request for the commits already on this branch. The title and body come from `pr-description`.

## When to use

- Commits exist on a non-default branch and a pull request is the next step
- The user asks to push a branch and open or update a PR
- A local branch is ahead of its upstream and the PR body is missing or stale

## When not to

- Nothing is committed — commit first (`commit-message`)
- The branch is the default branch (`main` or `master`) — do not open a PR from the base into itself
- The task is only writing the title and body — use `pr-description`
- The task is reviewing the diff for defects — use `code-review`
- The working tree has uncommitted changes that belong in the PR — commit or stash them first; do not push a half-finished tree

## Steps

1. Run `publish-check` on this repo before any `git add`, commit, or push. Stop if the check fails.
2. Confirm the branch:
   - `git status` is clean, or leftover files are intentionally left out
   - `git branch --show-current` is not the default branch
   - `git rev-parse --abbrev-ref @{upstream}` succeeds, or you know which remote to set
3. Read the range against the base. Default base is `main` unless the project says otherwise:
   - `git log --oneline <base>..HEAD`
   - `git diff <base>...HEAD`
   Stop if the range is empty.
4. Draft the title and body with `pr-description`. If the repo has a pull request template, fill that template.
5. Push the branch. If it has no upstream, set it on the first push:
   - `git push -u origin HEAD`
   Do not force-push unless the user explicitly asked to rewrite already-pushed commits.
6. Open or update the pull request with the GitHub CLI:
   - New: `gh pr create --base <base> --title "<title>" --body "<body>"`
   - Existing: `gh pr edit --title "<title>" --body "<body>"`
   Pass `--repo` only when the current checkout is not the target repository.
7. Print the PR URL from the command output. Do not invent a URL.

## Safety

- Push only the current feature branch. Never push the default branch as part of opening a PR.
- Do not use `--force` or `--force-with-lease` unless the user asked to update a rewritten branch.
- Do not put tokens, host paths, or local account names in the title, body, or command output you keep.
- If `gh` is not authenticated for this checkout, stop and say so. Do not switch accounts or run `gh auth login`.

## Example

Branch `feat/open-pr`, base `main`, one commit, clean tree:

```
git push -u origin HEAD
gh pr create --base main \
  --title "feat(skills): add open-pr workflow skill" \
  --body "$(cat <<'EOF'
## Summary

Adds a workflow skill that pushes the current branch and opens a pull request, and indexes it in the catalog.

## How to test

- Confirm skills/workflow/open-pr/SKILL.md frontmatter matches its path
- Confirm the catalog and README each have one row for open-pr
EOF
)"
```

## Done when

The branch is on the remote, a pull request exists against the base, and the printed URL is the one the CLI returned.
