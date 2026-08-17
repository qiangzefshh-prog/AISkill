---
name: wiki-page
description: Add, move, or remove a row in skills/catalog.md so the wiki index matches the tree.
category: authoring
tags: [catalog, index]
---

# wiki-page

`skills/catalog.md` is the wiki index. Categories are headings. Each skill is one table row.

## When to use

- A skill folder was added, renamed, moved, or deleted
- Tags or the one-line summary changed
- The catalog and the tree disagree

## Row format

```
| [name](category/name/SKILL.md) | tag-a, tag-b | One sentence |
```

- Link is relative to `skills/catalog.md`
- Tags match the skill frontmatter (comma-separated)
- Summary is one sentence, no trailing period required

## Steps

1. Open `skills/catalog.md`.
2. Find the heading for the skill’s `category`. If the category is new, add a heading plus a one-line purpose, then a table with columns Name / Tags / Summary.
3. Insert or edit the row in alphabetical order by `name` within that table.
4. If the skill moved category, delete the old row.
5. If the skill was deleted, delete the row. Remove an empty category heading.
6. Confirm every `skills/<category>/<name>/SKILL.md` has exactly one row.

## Done when

`catalog.md` lists the same set of skills as the directories under `skills/`, excluding `catalog.md` itself.
