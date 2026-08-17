---
name: issue-triage
description: Classify a GitHub issue from its title, body, and labels so it can be routed.
category: workflow
tags: [github, labels]
---

# issue-triage

Sort one issue. Do not implement it here.

## When to use

- A new issue arrived
- The issue has no type label
- Several issues need a first pass

## Labels (suggested)

| Label | Use when |
| --- | --- |
| `skill` | Request or bug about a specific `SKILL.md` |
| `catalog` | Index / category / tag problem |
| `docs` | README or AGENTS wording |
| `good first issue` | Small, self-contained, no design debate |

Add a skill name in the title or first comment when the issue points at one folder.

## Steps

1. Read title and body. Ignore screenshots unless they are the only content.
2. Decide type: new skill, fix existing skill, catalog drift, docs, or not-this-repo.
3. Apply one primary label from the table. Add `good first issue` only if the change is a single file.
4. If the request is a new skill, say which `category` it belongs in, or that a new category needs a reason.
5. If it is not a skill-catalog problem, close or redirect with one sentence.

## Done when

The issue has a type label and a one-line routing note (category or “not this repo”).
