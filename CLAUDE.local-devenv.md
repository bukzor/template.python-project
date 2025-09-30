## Next Major Feature: Local DevEnv Package Architecture

### Problem

Current approach puts all dev dependencies (baseline CI tooling + user deps) in
one `pyproject.toml`. When users run `copier update`, their custom dependencies
get overwritten.

### Solution: lib/local-devenv Sub-package

Create a controlled sub-package that copier can fully manage, separate from
user's application dependencies.

### Architecture

For multi-language support, organize by language under
`lib/local-devenv/{lang}/`:

```
my-project/
├── pyproject.toml                    # User-controlled (app deps, custom dev deps)
├── lib/
│   └── local-devenv/                # Template-controlled (copier owns this entirely)
│       ├── python/                  # Python baseline tooling
│       │   └── pyproject.toml       # black, pyright, copier, etc.
│       ├── node/                    # Node.js baseline tooling (future)
│       │   └── package.json         # prettier, eslint, etc.
│       └── rust/                    # Rust baseline tooling (future)
│           └── Cargo.toml           # clippy, rustfmt, etc.
├── src/my_project/                  # User's application code
└── ...
```

### Implementation Plan

1. **Create lib/local-devenv structure in template**
   - `copier-template/lib/local-devenv/python/pyproject.toml.jinja`
   - Move all baseline dev deps there
   - Add node/ and rust/ directories later as needed

2. **Update root template pyproject.toml**
   - Remove baseline dev deps
   - Add `"./lib/local-devenv/python"` as dev dependency
   - Keep structure for user's own dependencies

3. **Update copier configuration**
   - Ensure lib/local-devenv/python gets fully managed by template
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
  "./lib/local-devenv/python", # Template-provided Python tooling
  # User adds additional dev deps here
]
```

### Template's lib/local-devenv/python/pyproject.toml:

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
  # ... all baseline Python tooling
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

## Future: Dhall + .templated/ Pattern for Config Generation

### Problem

Most config systems lack include/extends functionality (pyproject.toml,
package.json, Cargo.toml, etc.), creating template vs. user customization
conflicts beyond just dependency management.

### Solution: Dhall + Read-Only Generated Configs

Use Dhall to generate configs from composable sources, commit both source and
generated files.

### Convention

```
.vscode/.templated/settings.json.dhall  → .vscode/settings.json
./.templated/pyproject.toml.dhall        → ./pyproject.toml
lib/local-devenv/.templated/pyproject.toml.dhall → lib/local-devenv/pyproject.toml
```

### Workflow

1. Template provides base `.dhall` files (template defaults + user import)
2. User edits user-specific `.dhall` files (their customizations)
3. Build generates config files with `chmod 444` (read-only)
4. Commit both `.dhall` source files AND generated configs

### Benefits

- **Drive-by contributors** see normal config files, work as expected
- **Read-only protection** prevents accidental direct edits
- **Git diffs** show both source changes and results
- **No extra tools** for casual users (dhall only needed when changing config)
- **Universal solution** for any config splitting need (template/user,
  environment, team/personal)

### Integration with local-devenv

- Copier handles project scaffolding and major updates
- Dhall system handles ongoing config evolution within projects
- Complementary, not competing approaches
