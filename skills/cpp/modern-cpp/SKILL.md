---
name: modern-cpp
description: Write or edit C++ so ownership, lifetime, and const are visible in the types. Use when adding or changing C++ sources.
category: cpp
tags: [cxx, raii, ownership]
---

# modern-cpp

Prefer the type system over comments. Do not invent a second style guide if the repo already has one.

## When to use

- Adding or rewriting C++ (`.cpp`, `.cc`, `.cxx`, `.hpp`, `.h` used as C++)
- A change copies, locks, or allocates and the owner is unclear
- Code uses raw `new`/`delete`, C arrays, or non-const where mutation is not required

## Defaults

Follow the project’s existing dialect (C++17/20/23, clang-format, IWYU). If none is stated:

- C++17 or newer
- RAII for every resource (memory, fd, lock, handle)
- `const` by default; `noexcept` only when it is true
- no file-scope `using namespace`

## Steps

1. Read neighboring headers and the build file. Match include style, namespace, and error policy (`exceptions` vs `std::expected` / error codes).
2. Put ownership in the signature:
   - transfer: `T` by value or `std::unique_ptr<T>`
   - share: `std::shared_ptr<T>` only when lifetime is shared
   - read: `const T&` or `std::span<const T>`
   - mutate: `T&` or `std::span<T>`
   - optional: `std::optional<T>` or nullable `T*`
3. Initialize everything at declaration. Prefer `{}` and member initializers over assignment in the constructor body.
4. Replace `new`/`delete` with `std::make_unique` / containers. Replace C arrays with `std::array` or `std::vector`. Replace pointer arithmetic with `std::span`.
5. Keep headers minimal: include what you use, forward-declare in `.h` when a pointer/reference is enough, put non-template bodies in `.cpp`.
6. Do not introduce UB: no dangling refs, no uninit reads, no signed overflow, no data races. Prefer `std::move` only on locals you will not use again.
7. Build the target you touched. If sanitizer flags exist, leave them on.

## Example

```cpp
// transfer
std::unique_ptr<Foo> make_foo(Config cfg);

// read without copy
void render(const Scene& scene, std::span<const Draw> draws);

// mutate in place
void sort_in_place(std::span<Item> items);
```

## Done when

The change compiles, ownership is readable from signatures, and no new raw resource management or UB-prone pattern was added.
