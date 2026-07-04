---
managed-by: Skill(llm-subtask)
status: open
cost-benefit-sweh:
  timebox:
    "@value": 3
    rationale:
      copier question + lib scaffold (build-system, package layout) +
      copier-update validation against basedpyright consumer
    confidence: unsure
  benefit-2w:
    "@value": 1
    rationale:
      unblocks library scaffolds; basedpyright already hand-converted, next lib
      consumer within 2w uncertain
    confidence: tentative
---

# copier `project_type: app | lib` question

**Priority:** Medium **Complexity:** Medium **Context:** Surfaced while
scaffolding `basedpyright-as-pyright` (ADR
`basedpyright-as-pyright/docs/adr/0001-redirect-pyright-engine-to-a-fork.md`),
the first concrete _library_ consumer of this template.

## Problem Statement

The template scaffolds **app-form only**: a project that runs but cannot be
built, installed, or imported as a distribution. There is no path to a
**library** — an installable, importable package — so library projects must
hand-convert the scaffold output, defeating the point of the template.

## Current Situation (evidence)

In `copier-template/`:

- `pyproject.toml.jinja` has **no `[build-system]`** → the project is not a
  buildable/installable distribution.
- The only code file is a root `main.py` with a `main()` that prints hello → an
  executable entrypoint, not a package. No `src/<slug>/__init__.py`.
- No `[project.scripts]`; `dependencies = []`.
- `copier.yml` computes `project_slug`/`underscored` (the would-be package name)
  but **never creates a package directory from it** — the lib affordance is
  half-stubbed and unused.

---

## Requirements (bukzor)

> Owner's requirements. **[explicit]** = stated in conversation; **[inferred]**
> = derived from context, not stated verbatim — confirm before relying on these.

- [ ] **[explicit]** The template must support **library** projects, not just
      apps ("make it library compatible").
- [ ] **[explicit]** The mechanism is a copier **`project_type: app | lib`**
      question. (User: "right fix is a copier `project_type: app | lib` question
      — that's the content of the todo.")
- [ ] **[inferred]** `app` remains the **current default behavior** (root
      `main.py`, no build-system); the change is additive, existing app
      scaffolds unaffected.
- [ ] **[inferred]** `lib` must produce a **pip/uv-installable distribution** —
      driven by `basedpyright-as-pyright`'s need to ship a `.pth` recorded in
      `RECORD` and removed by `pip uninstall` (requires a real build-system).

---

## Recommendations (Claude)

> My design suggestions for _how_ to satisfy the requirements above. Not
> owner-blessed; up for revision.

- [ ] Add `project_type: {type: str, choices: [app, lib], default: app}` to
      `copier.yml`.
- [ ] **lib** branch generates:
  - [ ] `[build-system]` using **hatchling** (matches the ADR's `force-include`
        mechanism; consistent with the repo's existing tooling).
  - [ ] a `src/{{ project_slug }}/__init__.py` package (src-layout).
  - [ ] optional `[project.scripts]` entrypoint wired to the package.
- [ ] **app** branch keeps today's `main.py` + no build-system, unchanged.
- [ ] Gate templated files on `project_type` (copier `{% if %}` or conditional
      file inclusion) so each branch emits only its own layout.

## Open Questions

- [ ] src-layout (`src/pkg/`) vs flat-layout (`pkg/`) for the lib branch?
- [ ] Should `lib` also offer an app-style entrypoint, or are they exclusive?
- [ ] Does anything in CI (`.github/workflows/*`, `pytest --doctest-modules`)
      assume `main.py` exists and need a `project_type` guard?

## Success Criteria

- [ ] `copier copy` with `project_type=lib` yields a project that `uv build` /
      `pip install .` succeeds on and is importable.
- [ ] `project_type=app` output is byte-identical to today's scaffold.
- [ ] `basedpyright-as-pyright` can scaffold from `lib` without hand-editing the
      build-system or package layout.

## Notes

The ADR's "honor the template conventions" line is currently unsatisfiable for
the lib bits — the template can't supply build-system/package-dir/force-include,
so that project must _add_ them. This TODO closes that gap upstream so future
library projects inherit it instead of re-deriving it.
