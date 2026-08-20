---
name: cmake-build
description: Configure, build, and test a C/C++ tree with the project’s CMake (or equivalent) without hard-coding host paths.
category: cpp
tags: [cmake, build, ctest]
---

# cmake-build

Use the repo’s build files. Do not drop in a new generator unless the project has none.

## When to use

- Need to compile, link, or run tests after a C/C++ edit
- CMake / Meson / Bazel files are part of the change
- A “works on my machine” path or compiler flag is about to be committed

## Steps

1. Find the build entry: `CMakeLists.txt`, `meson.build`, `Makefile`, or a documented wrapper (`cmake --preset`, `scripts/build`). Read it before adding flags.
2. Prefer an out-of-source build (`build/`, `out/`, or the preset’s binary dir). Do not in-source configure unless the project already does.
3. Configure with the project’s mechanism:
   - presets: `cmake --preset <name>`
   - otherwise: `cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug`
   - do not embed `/home/…`, `/Users/…`, or machine-specific SDK roots in tracked files
4. Build only the target you need: `cmake --build build --target <name>`. Match the existing generator (Ninja if `build.ninja` is already there).
5. Run tests the same way CI does (`ctest --test-dir build`, `cmake --build build --target test`, or the script in README). Do not invent a second runner.
6. If you add sources, update the build list (`add_library`/`target_sources`) in the same change. Keep include dirs on the target (`target_include_directories`), not global.
7. New compile options go on the relevant target (`target_compile_features`, `target_compile_options`). Do not `add_definitions` globally.

## Guardrails

- Tracked CMake must not require a private toolchain file
- Generator expressions over hard-coded `/usr/local`
- `FetchContent` / vendored deps stay reproducible (pinned tag or hash)

## Done when

Configure + build + the relevant tests pass, and no host path or one-off flag landed in a committed file.
