---
name: cpp-debug
description: Reproduce a C/C++ crash or wrong result with sanitizers and a debugger before changing code at random.
category: cpp
tags: [asan, ubsan, gdb]
---

# cpp-debug

Reproduce first. Guess last. Do not silence a sanitizer to make the log clean.

## When to use

- Crash, hang, wrong output, or flaky test in C/C++
- A change “works” but ASan/UBSan/TSan was not run
- Need a stack, watchpoint, or race report

## Steps

1. Get a reliable repro: exact target, args, input file, and build type (`Debug`). One-command repro, written down.
2. Rebuild with the project’s sanitizer options if they exist. Otherwise, for a local Debug build:
   - memory/lifetime: AddressSanitizer + UndefinedBehaviorSanitizer
   - data races: ThreadSanitizer (not combined with ASan)
   - leaks: ASan leak detection or standalone LSan
3. Run the repro under the sanitizer. Save the full report (stack, allocation site, thread ids). That report is the spec for the fix.
4. If the sanitizer is silent, use the debugger (`gdb`/`lldb`) on the same binary:
   - break on the failing function or `catch throw`
   - print the span/size/owner at the fault
   - for hangs, `thread apply all bt` (gdb) or `bt all` (lldb)
5. Fix the root cause (lifetime, bounds, race, uninit). Add a regression test that failed before the fix.
6. Re-run the sanitizer build. Then run the normal test set the project already uses.

## Guardrails

- Do not add `-fno-sanitize=…`, `ASAN_OPTIONS=detect_leaks=0`, or `#ifndef SANITIZE` to hide a bug
- Do not ship a “fix” that only changes timing (`sleep`, extra log) unless the bug was a documented race and the real fix is synchronization
- Do not commit sanitizer suppressions without naming the bug they cover

## Done when

The original repro is green under the relevant sanitizer, a test covers it, and no sanitizer flag was weakened.
