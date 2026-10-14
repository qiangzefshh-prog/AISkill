---
name: changelog
description: Draft a changelog section from conventional commits since the last release. Use when cutting a release note or updating CHANGELOG.
category: workflow
tags: [changelog, release, conventional-commits]
---

# changelog

Group shipped commits into a release note. Do not invent entries the history does not contain.

## When to use

- Preparing a release note or a `CHANGELOG` section
- The user asks what changed since a tag or date
- Conventional commits exist and need to be turned into user-facing notes

## When not to

- Writing a single commit message — use `commit-message`
- Writing a pull request body — use `pr-description`
- There is no commit range (uncommitted work only)

## Steps

1. Find the range. Last release tag if one exists (`git describe --tags --abbrev=0`), otherwise the range the user named. List commits with `git log --oneline <from>..HEAD`.
2. Skip `chore`, merge commits, and reverts that cancel an earlier commit in the same range. Keep `feat`, `fix`, `docs`, `refactor`, and anything marked breaking.
3. Group under these headings, omitting empty ones:
   - **Breaking**
   - **Added** (`feat`)
   - **Fixed** (`fix`)
   - **Changed** (`refactor` and behavior-preserving updates worth mentioning)
   - **Docs** (`docs`, only if the project publishes doc changes)
4. Rewrite each subject as a user-facing sentence. Drop the type prefix and ticket-only subjects (`fix: wip`). Link the short hash when the project already does.
5. Put the version or date the user asked for at the top. Do not bump a version that was not requested.
6. If a `CHANGELOG` or release-notes file already exists, match its heading style and prepend the new section. Do not restyle older entries.

## Example

```
## Unreleased

### Added

- Workflow skill to draft a changelog from conventional commits

### Fixed

- Catalog row for a renamed skill pointed at the old path
```

## Done when

Every bullet maps to a commit in the range, empty groups are omitted, and the section matches the existing changelog style if one exists.
