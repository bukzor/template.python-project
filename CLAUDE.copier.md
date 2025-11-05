# Copier Template Implementation Project

## Overview

Converting a Python project template from static GitHub template repository to a
dynamic copier-based template that supports:

1. User-defined placeholders
2. Acceptance testing of the template

## Current Status

### Completed ✅

- Created `copier.yml` configuration with template variables
- Created `lib/ci/copier` script for both CI and interactive use
- Restructured project files into `{{project_name}}/` template directory
- Replaced `{{PROJECT_NAME}}` placeholders with `{{project_name}}` copier
  variables
- Created GitHub Actions workflows (`setup.yml`, `test-template.yml`)
- Created test input file (`input-for-test.yml`)
- Template generation needs verification

### Issue to Investigate 🔍

Template generation may not be working as expected. Test with the command below
and verify output.

## Project Structure

```
template.python-project/
├── copier.yml                           # Copier configuration
├── lib/ci/copier                        # Script for template generation
├── copier-template/                     # Template directory (gets copied to new projects)
│   ├── pyproject.toml.jinja             # Template files with variables
│   ├── CLAUDE.md.jinja
│   ├── README.md.jinja
│   └── ... (other project template files)
├── .github/workflows/
│   ├── setup.yml                        # Auto-templating on GitHub
│   └── test-template.yml                # Template acceptance testing
└── ... (development files - NOT copied to generated projects)
```

## Key References

### Simon Willison's Dynamic Template Pattern

- **Blog post**:
  https://simonwillison.net/2021/Aug/28/dynamic-github-repository-templates/
- **Template repo**: https://github.com/simonw/python-lib-template-repository
- **Cookiecutter**: https://github.com/simonw/python-lib

**Key insights**:

- Uses GitHub Actions to fetch repo metadata via GraphQL
- Calls cookiecutter/copier with dynamic variables
- Force pushes generated content back to repo
- Self-deletes the setup workflow

### Copier Documentation

- **Cloned locally**: `trash/copier/`
- **Key docs**: `trash/copier/docs/configuring.md`
- **README quick-start**: `trash/copier/README.md` (lines ~50-80) - Shows
  `{{project_name}}/` directory structure
- **Exclude examples**: `trash/copier/tests/demo_exclude/copier.yml` - Shows
  `_exclude` usage
- **Subdirectory examples**: Search `trash/copier/docs/configuring.md` for
  `_subdirectory` and `python_engine` example

## Current copier.yml Configuration

```yaml
# Use the copier-template subdirectory as the actual template
_subdirectory: copier-template
project_name:
  type: str
  help: What is your project name?
  # ... other variables
```

## Configuration Notes

Current `copier.yml` uses `_subdirectory: copier-template`. This keeps the
template source files cleanly separated from the repository's own development
files (CI scripts, documentation about the template itself, etc.).

## Test Command

```bash
# Test template generation
./lib/ci/copier --no-input --name test-project --description "Testing the copier template" --destination trash/test-copier-template

# Check what was generated
ls -la trash/test-copier-template/
```

## References for Tomorrow

### Most Helpful Documentation

- `trash/copier/README.md` (lines 50-80) - Quick-start showing
  `{{project_name}}/` structure
- `trash/copier/docs/configuring.md` - Search for `_subdirectory` and
  `python_engine` example
- `trash/copier/tests/demo_exclude/copier.yml` - `_exclude` pattern
- `trash/python-lib/` - Simon's clean cookiecutter template structure for
  comparison

### Key Files to Check

- `copier.yml` - Current configuration
- `copier-template/` - Template files (correctly structured)
- `lib/ci/copier` - Working script for template generation

### Next Steps

1. Test template generation and verify output
2. Adjust configuration if needed
3. Test the GitHub Actions workflows
4. Document the final solution

## Success Criteria

- Template generation produces expected project structure
- All template variables are correctly resolved
- GitHub Actions workflow works for auto-templating
- Template can be tested locally and in CI
