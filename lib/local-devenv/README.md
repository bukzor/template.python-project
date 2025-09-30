# local-devenv

The `local-devenv` package contains all baseline development tooling
(formatters, linters, type checkers, etc.) managed by the project template. This
separation allows:

- **Template updates preserve user customizations**: When you run
  `copier update`, your custom dependencies in the root `pyproject.toml` won't
  be overwritten
- **Consistent tooling**: All baseline dev tools are versioned together by the
  template
- **Simple workflow**: Still just `uv sync` to install everything

Your root `pyproject.toml` references it as:

```toml
[dependency-groups]
dev = [
  "./lib/local-devenv", # Template-managed tooling
  # Your custom dev dependencies here
]
```
