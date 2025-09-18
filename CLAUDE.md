# Claude Setup Instructions

This is a Python project template optimized for Claude Code development.

## Quick Start

After creating a new repo from this template:

```bash
# Initialize the project (replace placeholders in pyproject.toml)
uv init . --name your-project-name

# Install development dependencies
uv add --dev pyright black pre-commit

# Install pre-commit hooks
uv run pre-commit install

# Test the setup
uv run pre-commit run --all-files
```

## Development Commands

- **Format code**: `uv run black .`
- **Type check**: `uv run pyright`
- **Run pre-commit**: `uv run pre-commit run`
- **Install package in dev mode**: `uv pip install -e .`

## Features Included

- ✅ **Pyright** in strict mode for type checking
- ✅ **Black** for code formatting
- ✅ **Pre-commit hooks** using `uv run` for consistent tooling
- ✅ **direnv** support with `.envrc`
- ✅ **Minimal gitignore** with only build products
- ✅ **Python 3.13+** requirement

## Template Customization

1. Replace `{{PROJECT_NAME}}` in `pyproject.toml`
2. Replace `{{PROJECT_DESCRIPTION}}` in `pyproject.toml`
3. Rename `README.template.md` to `README.md` and customize
4. Add your project-specific dependencies to `pyproject.toml`

## Pre-commit Hooks

The template includes local pre-commit hooks that use `uv run` to ensure consistent virtual environment usage:

- **black**: Auto-formats Python code
- **pyright**: Type checking (runs on whole repo for thorough checking)

Both hooks will run before every commit to maintain code quality.