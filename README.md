# Python Project Template

A [copier](https://copier.readthedocs.io/) template for Python projects with
modern tooling and best practices.

## Features

- **Python 3.10+** with configurable minimum version
- **[uv](https://github.com/astral-sh/uv)** for fast dependency management
- **[Black](https://black.readthedocs.io/)** for code formatting
- **[Pyright](https://github.com/microsoft/pyright)** in strict mode for type
  checking
- **[pre-commit](https://pre-commit.com/)** hooks integrated with uv
- **direnv** support with `.envrc`
- **Local development environment** package structure (`lib/local-devenv/`)

## Using This Template

Create a new project from this template:

```bash
# Using copier
copier copy gh:bukzor/template.python-project your-project-name
cd your-project-name

# Install dependencies and hooks
uv sync
uv run pre-commit install

# Verify setup
uv run pre-commit run --all-files
```

## Template Development

This repository is also an instance of itself (dogfooding). To develop the
template:

```bash
# Clone the template repository
git clone https://github.com/bukzor/template.python-project
cd template.python-project

# Install dependencies
uv sync

# Run acceptance tests
./lib/ci/acceptance-test

# Test template generation
./lib/ci/copier
```

The template source lives in `copier-template/`. Changes there affect newly
generated projects.

## What Gets Generated

Projects created from this template include:

- `pyproject.toml` - Python project configuration with development dependencies
- `.pre-commit-config.yaml` - Pre-commit hooks for black and pyright
- `main.py` - Simple starter file
- `lib/local-devenv/` - Template-managed development tooling (future feature)
- `.envrc` - direnv configuration for automatic environment activation
- CI workflows for testing

## License

MIT License
