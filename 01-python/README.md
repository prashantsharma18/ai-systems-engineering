# 01 — Python

Python as an engineering discipline, not just a scripting language. This section covers the language features, idioms, and patterns that matter most for ML and AI systems work.

## Sub-folders

| Folder | Notes | Notebooks | Status |
|--------|-------|-----------|--------|
| [fundamentals/](./fundamentals/) | Data structures, decorators, generators, comprehensions | `data-structures.ipynb`, `decorators-and-closures.ipynb`, `comprehensions-generators.ipynb` | In Progress |
| [best-practices/](./best-practices/) | Type hints, protocols, testing with pytest, project layout | `type-hints-and-protocols.ipynb`, `testing-with-pytest.ipynb` | Planned |
| [patterns/](./patterns/) | Functional patterns, OOP for ML, async patterns | `functional-patterns.ipynb`, `oop-for-ml.ipynb`, `async-patterns.ipynb` | Planned |

## Blog Posts

| Title | Status |
|-------|--------|
| [Python for ML Engineers](./blogs/python-for-ml-engineers.md) | Draft |

## Why This Matters

Most ML courses skip over Python internals. Understanding how Python's data model works, when to use generators vs lists, and how to write type-safe code makes the difference between scripts that work once and systems that hold up in production.

## Field Notes

### Topic 0 — Environment Setup
*2026-03-14*

The actual setup was faster than expected once `uv` was already in place — installing Python 3.11, creating the venv, and getting 123 packages into it took under a minute of real work. The interesting part is what this setup makes possible: a clean, isolated 3.11 environment means every subsequent topic starts from a known state, no system Python leaking in. The choice to pin 3.11 over 3.13 (which was already cached) is the same reasoning you'd use in production — compatibility over novelty when the downstream dependencies are what matter.
