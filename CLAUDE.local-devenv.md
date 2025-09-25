## Next Major Feature: Local DevEnv Package Architecture

### Problem

Current approach puts all dev dependencies (baseline CI tooling + user deps) in
one `pyproject.toml`. When users run `copier update`, their custom dependencies
get overwritten.

### Solution: lib/local-devenv Sub-package

Create a controlled sub-package that copier can fully manage, separate from
user's application dependencies.

### Architecture

```
my-project/
├── pyproject.toml                    # User-controlled (app deps, custom dev deps)
├── lib/
│   └── local-devenv/                # Template-controlled (copier owns this entirely)
│       ├── pyproject.toml           # Baseline dev tooling (black, pyright, copier, etc.)
│       └── __init__.py              # Makes it a package
├── src/my_project/                  # User's application code
└── ...
```

### Implementation Plan

1. **Create lib/local-devenv structure in template**
   - `copier-template/lib/local-devenv/pyproject.toml.jinja`
   - `copier-template/lib/local-devenv/__init__.py`
   - Move all baseline dev deps there

2. **Update root template pyproject.toml**
   - Remove baseline dev deps
   - Add `"./lib/local-devenv"` as dev dependency
   - Keep structure for user's own dependencies

3. **Update copier configuration**
   - Ensure lib/local-devenv gets fully managed by template
   - Root pyproject.toml can be customized by users

### Benefits

- Clean separation: template controls tooling, user controls app
- `copier update` won't overwrite user's custom dependencies
- User can still access all template tooling via local package
- Maintains single `uv sync` workflow

### Root pyproject.toml would look like:

```toml
[project]
name = "{{project_name}}"
dependencies = [
  # User adds their app dependencies here
]

[dependency-groups]
dev = [
  "./lib/local-devenv", # Template-provided tooling
  # User adds additional dev deps here
]
```

### Template's lib/local-devenv/pyproject.toml:

```toml
[project]
name = "local-devenv"
dependencies = []

[dependency-groups]
dev = [
  "black>=25.1.0",
  "copier>=9.4.1",
  "pyright>=1.1.405",
  "pre-commit>=4.3.0",
  # ... all baseline tooling
]
```

### Testing Strategy

1. Generate project with current approach
2. User adds custom dependencies to root
3. Run `copier update`
4. Verify user deps preserved, template tooling updated
5. Verify `uv sync && uv run black .` still works

### Files to Create/Modify

- `copier-template/lib/local-devenv/pyproject.toml.jinja`
- `copier-template/lib/local-devenv/__init__.py`
- `copier-template/pyproject.toml.jinja` (remove baseline deps)
- Test with acceptance test script
