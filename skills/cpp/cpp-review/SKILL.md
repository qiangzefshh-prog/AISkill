---
name: cpp-review
description: Review a C/C++ diff for UB, lifetime bugs, races, and API leaks. Use on C or C++ patches after the code is written.
category: cpp
tags: [review, ub, safety]
---

# cpp-review

Review the patch, not the idea of the patch. Language issues first, then style.

## When to use

- A PR or local diff touches `.c`, `.h`, `.cpp`, `.hpp`, or build files
- Sanitizers are not in the loop yet
- Ownership or thread-safety of a change is unclear

## Look at

1. **UB** — uninit reads, signed overflow, invalid pointer arithmetic, strict-aliasing / type-punning without `memcpy`/`std::bit_cast`, use-after-free, iterator invalidation.
2. **Bounds** — C arrays, `sprintf`, `strcpy`, pointer+length pairs without a checked span, `operator[]` on unchecked indexes.
3. **Lifetime** — returned references/pointers to locals, `string_view`/`span` over temporaries, captured `this` in async callbacks.
4. **Ownership** — raw `new`/`delete`/`malloc`/`free` without a matching RAII owner; `unique_ptr` released into a C API without a documented free path.
5. **Concurrency** — shared mutable state without a mutex/atomics story; locking order; `std::thread` without join/detach policy.
6. **API / ABI** — headers that allocate in one TU and free in another with different CRTs; exception crossing an `extern "C"` boundary.
7. **Build** — new files missing from CMake; flags that hide bugs (`-fno-exceptions` mixed with throwing code, sanitizers stripped in Debug).

## Output

Write:

- **Summary** — what the C/C++ change does
- **Blockers** — UB, leaks, races, ABI breaks, missing build entries
- **Notes** — const, naming, include hygiene

Do not restyle the whole file. Do not “fix” sanitizer findings by disabling the sanitizer.

## Done when

Blockers are empty or filed as required changes, and the review named the functions that own the risky resources.
