# Python Basic Toolkit

Foundational Python utilities for scripting, automation, and data wrangling. These modules favor standard-library solutions and portability.

## Quickstart
1. Clone or download this repository.
2. Navigate to `Python/Basic/` and inspect the agent guidelines in `AGENTS.md`.
3. Use the `CoreCodeAgent` for new modules and `BaselineTestAgent` for tests to ensure compliance.

## Contents
- `scripts/` — command-line entry points.
- `utils/` — reusable helper modules with full type annotations.
- `tests/` — pytest-compatible suites covering each utility.

## Conventions
- Target Python 3.12.
- Depend only on the standard library.
- Every module must ship with docstrings and examples documented in the README.
