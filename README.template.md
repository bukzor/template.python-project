# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

## Installation

```bash
# Clone the repository
git clone https://github.com/bukzor/{{PROJECT_NAME}}
cd {{PROJECT_NAME}}

# Install dependencies
uv sync

# Install pre-commit hooks (optional but recommended)
uv run pre-commit install
```

## Usage

```bash
# Run the main script
uv run python main.py

# Or install and run as a package
uv pip install -e .
{{PROJECT_NAME}}
```

## Development

```bash
# Format code
uv run black .

# Type check
uv run pyright

# Run tests
uv run pytest

# Run pre-commit hooks
uv run pre-commit run --all-files
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run the development commands above
5. Submit a pull request

## License

MIT License (or your preferred license)