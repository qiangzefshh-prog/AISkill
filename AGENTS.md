# AGENTS.md

Rules for agents and humans working in this public skill catalog.

Read `skills/catalog.md` before adding or editing a skill.

## What this repo is

A wiki-style collection of standalone agent skills. Each skill is one folder with a `SKILL.md`. Skills are grouped by category under `skills/`. The catalog is the index.

## Layout

```
skills/
  catalog.md              # index: category + tags + one-line summary
  <category>/
    <skill-name>/
      SKILL.md
```

Current categories: `authoring`, `workflow`. Add a category only when several skills share a new purpose.

## SKILL.md shape

```yaml
---
name: skill-name
description: One or two sentences. What it does and when to use it.
category: authoring
tags: [tag-a, tag-b]
---
```

- `name` must match the folder name.
- `category` must match the parent folder.
- `tags` are lowercase kebab-case; keep them short.
- Body: purpose, when to use, steps, examples. No machine-local paths, no private accounts, no secrets.

## Catalog

Every new or renamed skill must get a row in `skills/catalog.md` under its category:

`name` · tags · one sentence · link to `SKILL.md`

Remove the row if the skill is deleted.

## What may be committed

Commit only:

- `README.md`, `AGENTS.md`, `LICENSE`, `.gitignore`
- files under `skills/`

Do **not** commit:

- `AGENTS.local.md` or any `*.local.md`
- agent harness dirs: `.opencode/`, `.claude/`, `.cursor/`, `.codex/`, `.github/copilot/`
- `.env`, `.env.*`, credentials, SSH keys, tokens
- editor/OS junk (`.DS_Store`, `Thumbs.db`)

If a local checkout has private agent notes, keep them in `AGENTS.local.md` (gitignored). Do not copy host paths, SSH hosts, or other-repo remotes into tracked files.

## Workflow

1. Add or edit `skills/<category>/<name>/SKILL.md`.
2. Update `skills/catalog.md`.
3. Run the checks in `skills/authoring/publish-check/SKILL.md`.
4. Commit with a conventional message (`feat(skills): …`, `docs: …`). See `skills/workflow/commit-message/SKILL.md`.
5. Push the branch / open a PR as the project requires.

Do not mix unrelated skills in one commit. Do not rewrite published skill names without a catalog redirect note.

## Review

Use `skills/workflow/code-review/SKILL.md` on the diff. Reject leaks of local config, secrets, or off-catalog skills.
