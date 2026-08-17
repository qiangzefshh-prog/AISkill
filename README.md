# AISkill

A small public catalog of standalone agent skills.

Browse by category in [`skills/catalog.md`](skills/catalog.md). Each skill is one folder with a `SKILL.md`. Copy a skill into your agent’s skills directory, or point the agent at this repo.

## Layout

```
skills/
  catalog.md                 # wiki index: category + tags
  authoring/                 # how to write and publish skills
  workflow/                  # git and review habits
```

## Skills

### authoring

| Skill | Tags | Summary |
| --- | --- | --- |
| [skill-authoring](skills/authoring/skill-authoring/SKILL.md) | writing, frontmatter | Write a skill that fits this catalog |
| [wiki-page](skills/authoring/wiki-page/SKILL.md) | catalog, index | Add or update a catalog row |
| [publish-check](skills/authoring/publish-check/SKILL.md) | safety, gitignore | Check a change before you commit |

### workflow

| Skill | Tags | Summary |
| --- | --- | --- |
| [commit-message](skills/workflow/commit-message/SKILL.md) | git, conventional-commits | Write a conventional commit |
| [code-review](skills/workflow/code-review/SKILL.md) | review, diff | Review a skill or docs diff |
| [issue-triage](skills/workflow/issue-triage/SKILL.md) | github, labels | Sort an issue by title and labels |

## Use a skill

1. Open `skills/catalog.md` and pick a name.
2. Read `skills/<category>/<name>/SKILL.md`.
3. Copy that folder into the skills path your agent already uses.

## Contribute

See [`AGENTS.md`](AGENTS.md). New skills go under a category folder and must get a catalog row. Do not commit local agent config or `*.local.md`.
