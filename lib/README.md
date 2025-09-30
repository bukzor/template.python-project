# lib/ Directory

This directory contains packages and shared utilities.

## Package Organization

### Single Language Packages

For packages using only one language, the package files live directly in the
package directory:

```
lib/
└── some-package/
    └── pyproject.toml    # Python package
```

### Multi-Language Packages

When a package supports multiple languages, use language-specific
subdirectories:

```
lib/
└── some-package/
    ├── python/
    │   └── pyproject.toml
    ├── node/
    │   └── package.json
    └── rust/
        └── Cargo.toml
```

### Migration Path

Packages naturally evolve from single-language to multi-language:

1. **Start simple**: Single language gets the package directory directly
2. **Refactor when needed**: Move to `{package}/{lang}/` subdirectories when
   adding a second language
3. **Maintain compatibility**: Update dependency references when restructuring
