---
name: publish-check
description: Scan a pending change for local-config leaks, secrets, and catalog drift before commit.
category: authoring
tags: [safety, gitignore]
---

# publish-check

Run this before every commit to this repo.

## When to use

- About to `git add` / `git commit`
- Reviewing a PR that adds files
- After generating files with an agent

## Allowed paths

- `README.md`, `AGENTS.md`, `LICENSE`, `.gitignore`
- anything under `skills/`

## Block the commit if any of these appear

- `AGENTS.local.md`, `*.local.md`
- `.opencode/`, `.claude/`, `.cursor/`, `.codex/`
- `.env`, `.env.*` (except a documented `.env.example` with no secrets)
- private keys, `id_*`, `*.pem`, tokens, `gho_`, `ghp_`
- absolute home paths (`/home/…`, `/Users/…`)
- SSH host aliases, other-repo remotes, or a second GitHub account
- files that exist on disk but are not in the catalog (new `SKILL.md` without a `catalog.md` row)

## Steps

1. `git status` and `git diff` (staged + unstaged).
2. Confirm every new path is in the allowed list.
3. Search the diff for the block list above.
4. If a `SKILL.md` changed, confirm frontmatter `name` / `category` match its path.
5. If a skill was added, renamed, or removed, confirm `skills/catalog.md` matches.
6. `git add` only the intended public files. Do not `git add -A` if ignored junk is sitting in the tree.

## Done when

The staged set is public skill/docs only, catalog matches the tree, and the diff has no local identity or secrets.
