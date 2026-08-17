---
name: code-review
description: Review a skill or docs diff for catalog fit, leaks, and clarity.
category: workflow
tags: [review, diff]
---

# code-review

Review the patch, not the idea of the patch.

## When to use

- A pull request or local diff adds or edits skills
- `publish-check` already ran or should be re-run

## Look at

1. **Scope** — only allowed public paths (see `publish-check`).
2. **Shape** — frontmatter present; `name` and `category` match the path; tags are short.
3. **Catalog** — new/renamed/removed skills have a matching `catalog.md` change.
4. **Leaks** — no local paths, accounts, remotes, keys, or harness dirs.
5. **Clarity** — an agent can follow the steps without this repo’s private checkout.
6. **Size** — one skill or one docs theme per change set.

## Output

Write:

- **Summary** — what the diff does, one or two sentences
- **Blockers** — must fix before merge (leaks, wrong path, missing catalog row)
- **Notes** — optional wording or tag nits

Do not rewrite the whole skill unless a blocker requires it.

## Done when

Blockers are empty or filed as required changes, and the catalog still matches the tree.
