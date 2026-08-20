---
name: c-interop
description: Keep C and C++ boundaries safe: ABI, extern C, headers that compile as both, and no exceptions across the fence.
category: cpp
tags: [c, abi, extern-c]
---

# c-interop

Treat the C/C++ edge as an ABI, not a convenience include.

## When to use

- A `.c` file must call C++, or C++ must call a C library
- A public header is included from both languages
- Wrapping a C API with RAII, or exposing a C API from a C++ library

## Rules

- C++ symbols that C must call: `extern "C"` and a C-compatible type (POD / opaque pointer), not `std::string`, templates, or references
- No exception crossing `extern "C"`. Catch at the boundary; return an error code or a documented sentinel
- Allocation pairing: whoever allocates documents who frees. Prefer caller-provided buffers or an explicit `*_destroy` in the same library
- Headers used as both C and C++: wrap C++-only parts in `__cplusplus`, use `extern "C"` guards, avoid C++ keywords as identifiers
- Opaque types: `typedef struct Foo Foo;` in the C header; definition only in the C++ TU
- Do not pass STL containers, non-trivial C++ objects, or `bool` bitfields across a stable C ABI

## Steps

1. Identify the boundary header (the one both languages include). Keep it C-parseable.
2. List the exchanged types. Each must have a defined size/alignment or be an opaque pointer.
3. If wrapping C in C++: one RAII type per C handle (`unique_ptr` with a custom deleter calling the C free function).
4. If exposing C from C++: a thin `.cpp` file with `extern "C"` functions; catch exceptions; do not leak C++ types into the header.
5. Build at least one C TU and one C++ TU against the same header in the same change.

## Example

```c
#ifdef __cplusplus
extern "C" {
#endif

typedef struct SkillEngine SkillEngine;
SkillEngine* skill_engine_new(void);
void skill_engine_free(SkillEngine* e);
int skill_engine_run(SkillEngine* e, const char* input, char* out, size_t out_n);

#ifdef __cplusplus
}
#endif
```

## Done when

Both a C and a C++ translation unit compile against the boundary, ownership of every handle is named, and exceptions cannot escape `extern "C"`.
