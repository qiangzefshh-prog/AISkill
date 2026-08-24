---
name: skill-authoring
description: Write a standalone SKILL.md that fits this catalog. Use when adding or rewriting a skill.
category: authoring
tags: [writing, frontmatter]
---

# skill-authoring

Write one skill as one folder. Do not invent a second index format. For the full add-to-git path, use `make-skill`.

## When to use

- A new skill is needed
- An existing skill is vague, too long, or missing frontmatter
- A skill drifted from its folder name or category

## When not to

- The task is one-off and will not be reused
- An existing skill already covers the steps
- The content is a machine path, private account, or other-repo remote
- There are no numbered steps an agent can follow yet

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
- `category` equals the parent folder (`authoring`, `workflow`, or `cpp` unless a new category is justified)
- `description` is one or two sentences, enough for an agent to decide to load it
- tags are short, lowercase, kebab-case
- body stays general: purpose, when, steps, examples
- no host paths, no private account names, no tokens, no other repos on the author’s machine

## Description

Write the description for the agent that chooses whether to load the skill:

- Sentence 1: what the skill does
- Sentence 2 (optional): when to use it
- Include the verbs or file types that should trigger a load
- Do not write filler (`helpful guide`, `best practices`, `comprehensive`)

## Quality

- Steps are numbered, short, and executable without this checkout’s private files
- `name` matches the folder; `category` matches the parent folder
- Tags are few and stable; do not duplicate the category as a tag unless it is also a search term
- Point to a sibling skill instead of copying it
- Body is one idea; split if two unrelated workflows share a folder

## Body outline

1. Title matching `name`
2. When to use
3. Steps (numbered, short)
4. Example (optional, small)
5. Done when (how to know it worked)

## Anti-patterns

- Missing frontmatter, or `name` / `category` that do not match the path
- A second wiki or index besides `skills/catalog.md`
- Copying `publish-check`, `wiki-page`, or `commit-message` into this file
- Host paths, SSH aliases, tokens, or harness dirs (`.opencode/`, `.claude/`, …)
- A wall of prose with no steps and no “done when”

## Example

```yaml
---
name: commit-message
description: Turn a staged diff into a short conventional commit message.
category: workflow
tags: [git, conventional-commits]
---
```

```markdown
# commit-message

Write the message from the staged diff, not from intent.

## When to use

- Staging is done and a commit is needed

## Steps

1. Read `git diff --cached`.
2. Pick one type and scope.
3. Write one imperative line, ≤72 characters.

## Done when

The first line matches `type(scope): summary`.
```

## After writing

1. Update `skills/catalog.md` (see `wiki-page`)
2. Run `publish-check` before commit
3. Ship with `make-skill` if this is a new or renamed skill
