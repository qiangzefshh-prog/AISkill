---
name: pr-description
description: Write a pull request title and body from the branch diff and commits. Use when opening or updating a PR.
category: workflow
tags: [github, pull-request]
---

# pr-description

Describe the change that is on the branch, not the plan that led to it.

## When to use

- A branch is ready to open as a pull request
- An existing PR body is stale after new commits
- The user asks for a PR title, summary, or description

## When not to

- Nothing is committed yet — commit first (`commit-message`)
- The task is reviewing the diff for defects — use `code-review`
- The repo has no remote and no PR is being opened

## Steps

1. Read the range against the base branch: `git log --oneline <base>..HEAD` and `git diff <base>...HEAD`. Default base is `main` unless the project says otherwise.
2. Title: one imperative line, ≤72 characters. Prefer the same shape as a conventional commit (`type(scope): summary`) when the branch is one idea. Do not paste the branch name.
3. Body, in this order:
   - **Summary** — what changed, in a few sentences
   - **Why** — the problem or request, only if the diff does not make it obvious
   - **How to test** — commands or checks a reviewer can run; skip if there is nothing to run
4. Call out breaking changes, new dependencies, and migrations in their own short paragraph.
5. Do not list every file. Do not include host paths, tokens, or unrelated drive-by edits.
6. If the project already has a pull request template, fill that template instead of inventing a second layout.

## Example

```
feat(skills): add pr-description workflow skill

## Summary

Adds a workflow skill that turns a branch diff into a PR title and body, and indexes it in the catalog.

## How to test

- Confirm `skills/workflow/pr-description/SKILL.md` frontmatter matches its path
- Confirm the catalog and README each have one row for `pr-description`
```

## Done when

The title states the change, the body matches the diff (not a discarded plan), and a reviewer can tell what to look at without opening every file.
