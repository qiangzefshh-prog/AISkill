# Skill catalog

Index of every skill in this repo. Categories are folders under `skills/`. Tags are labels, not folders.

When you add, rename, or delete a skill, edit this file in the same change.

## authoring

How to write skills and keep the catalog honest.

| Name | Tags | Summary |
| --- | --- | --- |
| [skill-authoring](authoring/skill-authoring/SKILL.md) | writing, frontmatter | Write a `SKILL.md` that matches the catalog shape |
| [wiki-page](authoring/wiki-page/SKILL.md) | catalog, index | Add, move, or remove a catalog row |
| [publish-check](authoring/publish-check/SKILL.md) | safety, gitignore | Scan a change for leaks before commit |

## workflow

Everyday git and review work.

| Name | Tags | Summary |
| --- | --- | --- |
| [commit-message](workflow/commit-message/SKILL.md) | git, conventional-commits | Turn a diff into a conventional commit message |
| [code-review](workflow/code-review/SKILL.md) | review, diff | Review a skill or docs patch |
| [issue-triage](workflow/issue-triage/SKILL.md) | github, labels | Classify an issue from its title and labels |

## cpp

C and C++ work: write, build, review, debug, and the language boundary.

| Name | Tags | Summary |
| --- | --- | --- |
| [c-interop](cpp/c-interop/SKILL.md) | c, abi, extern-c | Keep C/C++ ABI, `extern "C"`, and dual-language headers safe |
| [cmake-build](cpp/cmake-build/SKILL.md) | cmake, build, ctest | Configure, build, and test without host paths |
| [cpp-debug](cpp/cpp-debug/SKILL.md) | asan, ubsan, gdb | Reproduce with sanitizers and a debugger before guessing |
| [cpp-review](cpp/cpp-review/SKILL.md) | review, ub, safety | Review a C/C++ diff for UB, lifetime, and races |
| [modern-cpp](cpp/modern-cpp/SKILL.md) | cxx, raii, ownership | Write C++ with ownership and const in the types |
