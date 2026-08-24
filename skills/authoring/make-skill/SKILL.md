---
name: make-skill
description: Add a catalog skill from idea through SKILL.md, catalog row, publish-check, commit, and push. Use when creating or shipping a new skill in this repo.
category: authoring
tags: [authoring, publish, git]
---

# make-skill

Ship one skill. Writing quality lives in `skill-authoring`; this file is the path from idea to git.

## When to use

- Adding a new skill folder to this repo
- Rewriting a skill that also needs a catalog or README change
- About to commit and push a skill change

## When not to

- Only editing prose inside an existing `SKILL.md` with no catalog drift — use `skill-authoring` then `publish-check`
- The work is not a skill (app code, harness config)

## Steps

1. Confirm it should be a skill (`skill-authoring`: when / when not).
2. Pick `category` and a lowercase kebab-case `name`. Add a category only when several skills share a new purpose.
3. Write `skills/<category>/<name>/SKILL.md` using `skill-authoring`.
4. Add or edit the row in `skills/catalog.md` (`wiki-page`). Keep `README.md` in the same change so both tables match.
5. Run `publish-check`. Fix leaks, path mismatches, and missing catalog rows before staging.
6. Stage only public files. Do not `git add -A` if ignored junk is in the tree.
7. Commit with `commit-message`, one idea per commit. Example: `feat(skills): add make-skill authoring skill`.
8. Push the current branch (`git push origin main` when working on `main`). Open a PR only if the project requires it.
9. Optional: run `code-review` on the diff before or after push.

## Example

New authoring skill `make-skill`:

```
skills/authoring/make-skill/SKILL.md
skills/catalog.md          # new row under authoring
README.md                  # same row in the authoring table
```

Then:

```
git add skills/authoring/make-skill/SKILL.md skills/catalog.md README.md
git commit -m "feat(skills): add make-skill authoring skill"
git push origin main
```

## Done when

The folder has a `SKILL.md`, `catalog.md` and `README.md` list it, `publish-check` is clean, and the commit is on the remote.
