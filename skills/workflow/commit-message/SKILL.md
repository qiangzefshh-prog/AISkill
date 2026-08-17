---
name: commit-message
description: Turn a staged diff into a short conventional commit message.
category: workflow
tags: [git, conventional-commits]
---

# commit-message

Write the message from the staged diff, not from intent.

## When to use

- Staging is done and a commit is needed
- A draft message is too vague (`update`, `fix`, `wip`)

## Format

```
type(scope): short summary
```

Types: `feat`, `fix`, `docs`, `refactor`, `chore`.

Scopes in this repo: `skills`, `catalog`, `docs`.

Summary: imperative, ≤72 characters, no trailing period.

## Steps

1. Read `git diff --cached` (or the full diff if nothing is staged yet).
2. Pick one type. Skill content → `feat(skills)`. Catalog-only → `docs(catalog)`. README/AGENTS → `docs`.
3. Name the skill or file in the summary when the change is narrow.
4. If the staged set mixes unrelated skills, split into two commits instead of writing “and”.
5. Do not mention the authoring tool in the message.

## Examples

```
feat(skills): add commit-message workflow skill
docs(catalog): index issue-triage
docs: describe catalog layout in README
```

## Done when

One commit would apply one idea, and the first line matches the format above.
