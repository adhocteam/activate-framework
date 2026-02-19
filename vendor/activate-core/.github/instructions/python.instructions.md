---
description: 'Python conventions and project-specific patterns'
applyTo: '**/*.py'
excludeAgent: []
---
# Python Instructions

Project-specific Python guidance. Only include what Copilot cannot infer from public documentation.

> **Note:** Do not restate PEP 8, standard library usage, or common patterns. Focus on your team's specific choices and constraints.

## Version and Runtime

<!-- CUSTOMIZE: Specify your Python version and any runtime constraints -->

- **Python version**: <!-- e.g., 3.11+, 3.12 required -->
- **Package manager**: <!-- e.g., Poetry, pip, uv -->
- **Virtual environment**: <!-- e.g., venv, conda, pyenv -->

## Tooling

<!-- CUSTOMIZE: List your specific tools and how to run them -->

| Tool | Command | Purpose |
|------|---------|---------|
| Formatter | <!-- e.g., `ruff format` --> | <!-- e.g., Code formatting --> |
| Linter | <!-- e.g., `ruff check` --> | <!-- e.g., Style and error checking --> |
| Type checker | <!-- e.g., `mypy .` --> | <!-- e.g., Static type analysis --> |
| Tests | <!-- e.g., `pytest` --> | <!-- e.g., Run test suite --> |

## Project Structure

<!-- CUSTOMIZE: Document your specific directory layout if it differs from conventions -->

```text
<!-- e.g.,
src/
├── api/           # FastAPI routes
├── services/      # Business logic
├── models/        # Pydantic models
└── repositories/  # Data access
-->
```

## Internal Libraries

<!-- CUSTOMIZE: List internal packages and their intended usage -->

<!-- e.g.,
- `adhoc-auth`: Use for all authentication; do not implement JWT handling directly
- `adhoc-logging`: Structured logging with correlation IDs; replaces stdlib logging
-->

## Team Conventions

<!-- CUSTOMIZE: Document decisions where multiple valid approaches exist -->

### Preferred Patterns

<!-- e.g.,
- Use `pathlib.Path` over `os.path` for file operations
- Use `httpx` over `requests` for HTTP clients (async support)
- Use Pydantic for data validation, not dataclasses
-->

### Patterns to Avoid

<!-- e.g.,
- Do not use `eval()` or `exec()` under any circumstances
- Avoid bare `except:` clauses; always specify exception types
- Do not use mutable default arguments
-->

## Type Hints

<!-- CUSTOMIZE: Specify your type hint expectations -->

<!-- e.g.,
- All public functions must have complete type annotations
- Use `from __future__ import annotations` for forward references
- Prefer `X | None` over `Optional[X]` (Python 3.10+ syntax)
-->

## Testing Conventions

<!-- CUSTOMIZE: Document your testing patterns -->

<!-- e.g.,
- Use pytest fixtures for database setup; see `conftest.py`
- Name test files `test_*.py`; name test functions `test_<behavior>_<condition>`
- Use `pytest-asyncio` for async tests with `@pytest.mark.asyncio`
-->

## Dependencies

<!-- CUSTOMIZE: Note any specific dependency decisions -->

<!-- e.g.,
- Pin all dependencies in `pyproject.toml`
- Run `pip-audit` before adding new packages
- Prefer stdlib solutions over adding new dependencies
-->
