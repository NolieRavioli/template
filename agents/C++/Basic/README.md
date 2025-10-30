# C++ Basic Modules

Modern C++20 building blocks maintained through coordinated AI agents.

## Quickstart
1. Consult `C++/Basic/AGENTS.md` for agent roles and statutes.
2. Use `SourceSmithAgent` for new source files and `ProofRunnerAgent` to add or update tests.
3. Validate builds with `cmake -S . -B build && cmake --build build` using `-DCMAKE_BUILD_TYPE=Debug`.

## Layout
- `src/` — production sources compiled into libraries or executables.
- `include/` — public headers with full documentation and self-contained dependencies.
- `tests/` — unit and integration tests using Catch2 or doctest.

## Quality Gates
- Enforce `clang-format` (Google style) before committing.
- Run `ctest --output-on-failure` under `-Wall -Wextra -Werror`.
- Apply sanitizers (`ASan`, `UBSan`) for nightly builds when feasible.
