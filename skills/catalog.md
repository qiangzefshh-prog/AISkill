# Skill catalog

Index of every skill in this repo. Categories are folders under `skills/`. Tags are labels, not folders.

When you add, rename, or delete a skill, edit this file in the same change.

## authoring

How to write skills and keep the catalog honest.

| Name | Tags | Summary |
| --- | --- | --- |
| [make-skill](authoring/make-skill/SKILL.md) | authoring, publish, git | Add a skill from idea through catalog, check, commit, and push |
| [publish-check](authoring/publish-check/SKILL.md) | safety, gitignore | Scan a change for leaks before commit |
| [skill-authoring](authoring/skill-authoring/SKILL.md) | writing, frontmatter | Write a `SKILL.md` that matches the catalog shape |
| [wiki-page](authoring/wiki-page/SKILL.md) | catalog, index | Add, move, or remove a catalog row |

## workflow

Everyday git and review work.

| Name | Tags | Summary |
| --- | --- | --- |
| [changelog](workflow/changelog/SKILL.md) | changelog, release, conventional-commits | Draft a changelog section from conventional commits since the last release |
| [code-review](workflow/code-review/SKILL.md) | review, diff | Review a skill or docs patch |
| [commit-message](workflow/commit-message/SKILL.md) | git, conventional-commits | Turn a diff into a conventional commit message |
| [git-bisect](workflow/git-bisect/SKILL.md) | git, bisect, debug | Find the commit that introduced a bug using binary search |
| [issue-triage](workflow/issue-triage/SKILL.md) | github, labels | Classify an issue from its title and labels |
| [open-pr](workflow/open-pr/SKILL.md) | github, pull-request, git | Push the current branch and open a pull request |
| [pr-description](workflow/pr-description/SKILL.md) | github, pull-request | Write a pull request title and body from the branch diff and commits |
| [tech-translation](workflow/tech-translation/SKILL.md) | translation, documentation, localization | Translate technical docs and strings while preserving structure and terminology |

## cpp

C and C++ work: write, build, review, debug, and the language boundary.

| Name | Tags | Summary |
| --- | --- | --- |
| [c-interop](cpp/c-interop/SKILL.md) | c, abi, extern-c | Keep C/C++ ABI, `extern "C"`, and dual-language headers safe |
| [cmake-build](cpp/cmake-build/SKILL.md) | cmake, build, ctest | Configure, build, and test without host paths |
| [cpp-debug](cpp/cpp-debug/SKILL.md) | asan, ubsan, gdb | Reproduce with sanitizers and a debugger before guessing |
| [cpp-review](cpp/cpp-review/SKILL.md) | review, ub, safety | Review a C/C++ diff for UB, lifetime, and races |
| [modern-cpp](cpp/modern-cpp/SKILL.md) | cxx, raii, ownership | Write C++ with ownership and const in the types |

## python

Python work: review patches and run tests the way the repo already does.

| Name | Tags | Summary |
| --- | --- | --- |
| [pytest](python/pytest/SKILL.md) | pytest, testing, python | Run and write pytest tests using the project’s existing config |
| [python-review](python/python-review/SKILL.md) | review, python, testing | Review a Python diff for bugs, API misuse, missing tests, and dependency changes |

## shell

Shell scripts: write portable scripts and review quoting, options, and injection.

| Name | Tags | Summary |
| --- | --- | --- |
| [shell-review](shell/shell-review/SKILL.md) | review, shell, quoting | Review a shell diff for quoting bugs, unsafe options, injection, and portability |
| [shell-script](shell/shell-script/SKILL.md) | shell, bash, posix | Write a portable POSIX or bash script with safe options and quoting |
