---
name: skill-authoring
description: Write a standalone SKILL.md that fits this catalog. Use when adding or rewriting a skill.
category: authoring
tags: [writing, frontmatter]
---

# skill-authoring

Write one skill as one folder. Do not invent a second index format.

## When to use

- A new skill is needed
- An existing skill is vague, too long, or missing frontmatter
- A skill drifted from its folder name or category

## Shape

Path: `skills/<category>/<name>/SKILL.md`

```yaml
---
name: skill-name
description: What it does and when to load it.
category: authoring
tags: [tag-a, tag-b]
---
```

Rules:

- `name` equals the folder name (lowercase kebab-case)
- `category` equals the parent folder (`authoring` or `workflow` unless a new category is justified)
- `description` is one or two sentences, enough for an agent to decide to load it
- tags are short, lowercase, kebab-case
- body stays general: purpose, when, steps, examples
- no host paths, no private account names, no tokens, no other repos on the author’s machine

## Body outline

1. Title matching `name`
2. When to use
3. Steps (numbered, short)
4. Example (optional, small)
5. Done when (how to know it worked)

## After writing

1. Update `skills/catalog.md` (see `wiki-page`)
2. Run `publish-check` before commit
