# Claude Setup Instructions

This repository is both:

1. A copier template for creating Python projects
2. A working instance of itself (dogfooding) for development and testing

## Quick Start

For template development:

```bash
# Install development dependencies
uv sync

# Install pre-commit hooks
uv run pre-commit install

# Test the setup
uv run pre-commit run --all-files

# Run acceptance tests
./lib/ci/acceptance-test
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

## Template Development

The template source files live in `copier-template/`. Changes there will affect
newly generated projects. This repository's root files are a generated instance
for testing the template output (dogfooding).

To modify the template, edit files in `copier-template/` and test with:

```bash
./lib/ci/copier
```

## Pre-commit Hooks

The template includes local pre-commit hooks that use `uv run` to ensure
consistent virtual environment usage:

- **black**: Auto-formats Python code
- **pyright**: Type checking (runs on whole repo for thorough checking)

Both hooks will run before every commit to maintain code quality.
