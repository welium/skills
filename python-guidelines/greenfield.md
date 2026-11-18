# Greenfield Project Dependencies and Tooling

Use `uv` for dependency management, lockfiles, virtual environments, running tools, and scripts.

Use these choices when the project needs them. Reuse an existing dependency when it fits.

* `httpx` for HTTP. Use `AsyncClient` for async workflows and `Client` for sequential work.
* Pydantic v2+ for validation and parsing.
* `pydantic-settings` for application settings when structured environment/config loading is required.
* Typer for non-trivial CLI applications.
* FastAPI for HTTP APIs.
* Plotly for interactive visualization.
* Loguru for application logging.
* Ruff for linting and formatting.
* Pyrefly for static type checking.

## Default Ruff and Pyrefly Configuration

When initializing a new project without existing configuration, use the following `pyproject.toml` template as a starting point. Adjust the configuration to suit the project's needs.

```toml
[tool.pyrefly]
preset = "strict"
min-severity = "warn"

[tool.ruff]
line-length = 100

[tool.ruff.lint]
select = [
    "E",    # pycodestyle errors
    "F",    # Pyflakes
    "I",    # isort
    "B",    # flake8-bugbear
    "UP",   # pyupgrade
    "SIM",  # flake8-simplify
    "RUF",  # Ruff-specific
]
ignore = [
    "E501", # formatter wraps where practical; line length is not a hard bound
]

[tool.ruff.format]
quote-style = "double"
indent-style = "space"
```
