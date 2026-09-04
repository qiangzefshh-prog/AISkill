# AISkill

A small public catalog of standalone agent skills.

Browse by category in [`skills/catalog.md`](skills/catalog.md). Each skill is one folder with a `SKILL.md`. Copy a skill into your agent’s skills directory, or point the agent at this repo.

## Layout

```
skills/
  catalog.md                 # wiki index: category + tags
  authoring/                 # how to write and publish skills
  workflow/                  # git and review habits
  cpp/                       # C and C++ write, build, review, debug
```

## Skills

### authoring

| Skill | Tags | Summary |
| --- | --- | --- |
| [make-skill](skills/authoring/make-skill/SKILL.md) | authoring, publish, git | Add a skill from idea through commit and push |
| [publish-check](skills/authoring/publish-check/SKILL.md) | safety, gitignore | Check a change before you commit |
| [skill-authoring](skills/authoring/skill-authoring/SKILL.md) | writing, frontmatter | Write a skill that fits this catalog |
| [wiki-page](skills/authoring/wiki-page/SKILL.md) | catalog, index | Add or update a catalog row |

### workflow

| Skill | Tags | Summary |
| --- | --- | --- |
| [commit-message](skills/workflow/commit-message/SKILL.md) | git, conventional-commits | Write a conventional commit |
| [code-review](skills/workflow/code-review/SKILL.md) | review, diff | Review a skill or docs diff |
| [git-bisect](skills/workflow/git-bisect/SKILL.md) | git, bisect, debug | Find the commit that introduced a bug using binary search |
| [issue-triage](skills/workflow/issue-triage/SKILL.md) | github, labels | Sort an issue by title and labels |
| [tech-translation](skills/workflow/tech-translation/SKILL.md) | translation, documentation, localization | Translate technical docs and strings while preserving structure and terminology |

### cpp

| Skill | Tags | Summary |
| --- | --- | --- |
| [c-interop](skills/cpp/c-interop/SKILL.md) | c, abi, extern-c | Keep C/C++ ABI and dual-language headers safe |
| [cmake-build](skills/cpp/cmake-build/SKILL.md) | cmake, build, ctest | Configure, build, and test without host paths |
| [cpp-debug](skills/cpp/cpp-debug/SKILL.md) | asan, ubsan, gdb | Reproduce with sanitizers before guessing |
| [cpp-review](skills/cpp/cpp-review/SKILL.md) | review, ub, safety | Review a C/C++ diff for UB and lifetime bugs |
| [modern-cpp](skills/cpp/modern-cpp/SKILL.md) | cxx, raii, ownership | Write C++ with ownership visible in the types |

## Use a skill

1. Open `skills/catalog.md` and pick a name.
2. Read `skills/<category>/<name>/SKILL.md`.
3. Copy that folder into the skills path your agent already uses.

## Contribute

See [`AGENTS.md`](AGENTS.md). New skills go under a category folder and must get a catalog row. Do not commit local agent config or `*.local.md`.
