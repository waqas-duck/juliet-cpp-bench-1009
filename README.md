# Juliet C++ benchmark subset

A curated subset of the NIST SARD **Juliet C/C++ 1.3** test suite (public domain), used as a labelled ground-truth target for measuring static-analysis detection on C++ code.

## Source

- Upstream mirror: https://github.com/arichardson/juliet-test-suite-c
- Upstream commit: `f88433e3443648a17671398797a04ea1f8e1a274`
- Original suite: NIST Software Assurance Reference Dataset (SARD), Juliet Test Suite for C/C++ v1.3. Juliet is a work of the US Government and is in the public domain.

## Contents

- `testcasesupport/`: the Juliet support headers and helpers (`std_testcase.h`, `std_testcase_io.h`, `std_thread.h`, `io.c`, `std_thread.c`) so testcase includes resolve.
- `testcases/CWE.../...`: 69 `.cpp` testcases, upstream layout preserved.

## Selection rule

- `.cpp` files only (C++ testcases, each wrapped in `namespace CWE..._01 { ... }`).
- Only the `_01` baseline flow variant (no control-flow or data-flow wrappers).
- At most 6 files per CWE, varying the source and sink where a CWE has many variants.
- CWEs chosen for C++ relevance: CWE762 mismatched memory management, CWE590 free of memory not on the heap, CWE401 memory leak (`new` variants), CWE415 double free, CWE416 use after free, CWE122 heap overflow (`cpp` and `placement_new` variants), CWE121 stack overflow (placement new), CWE124 / CWE126 / CWE127 buffer underwrite, overread and underread (`new` variants), CWE457 uninitialised variable, CWE476 NULL dereference, CWE23 / CWE36 path traversal, CWE680 integer overflow to buffer overflow (the suite has no `.cpp` variants of CWE78 or CWE190).

Each testcase has a `bad()` function whose flaw is marked with a `FLAW` or `POTENTIAL FLAW` comment, and `goodG2B()` / `goodB2G()` functions whose fixes are marked with `FIX` comments. The files are not meant to be built as one program; they are analysis targets.
