---
managed-by: Skill(llm-subtask)
status: open
---

# Harvest template improvements from the `basedpyright-as-pyright` diff

**Priority:** Medium **Complexity:** Low (mechanical, once the baseline exists)
**Context:** `basedpyright-as-pyright` is the first concrete _library_ consumer
scaffolded from this template. The delta between its pristine scaffold and its
finished state is direct evidence of template gaps.

## Problem Statement

Template gaps are invisible until a real project hits them. Rather than guess,
use the **exact diff** between what the template emitted and what the project
needed, and triage each divergence into the template.

## Prerequisite (must happen during the scaffold task — NOT recoverable later)

- [ ] In `basedpyright-as-pyright`: commit the **unedited copier output** as
      commit #1 and `git tag scaffold-baseline` _before any hand-edits_.
      (Tracked in ADR 0001 §Implementation.) Without this tag, the clean delta
      cannot be reconstructed — scaffold output and edits entangle.

## Procedure

- [ ] Read the full delta: `git diff scaffold-baseline..HEAD` in
      `basedpyright-as-pyright`.
- [ ] Triage **each hunk** into exactly one bucket:
  - [ ] **Upstream-generic** — every project would want it (e.g. having a
        build-system at all). → append to this repo's `todo.kb/` or open a PR.
  - [ ] **Parameterizable** — template-worthy but only for some projects (lib vs
        app; `force-include` of a `.pth`). → a copier _question_ (this is what
        `2026-06-24-000-copier-projecttype-app--lib-question.md` covers; fold
        new findings into it).
  - [ ] **Project-specific** — belongs only there (meta-path finder, the
        `pyright._utils` seam). → leave local, do not upstream.
- [ ] Apply the upstream-generic + parameterizable changes to the template.
- [ ] **Close the loop:** run `copier update` inside `basedpyright-as-pyright`.
      If it merges cleanly and the project still builds, the template change is
      validated against a real consumer.

## Confirmed findings (from the basedpyright-as-pyright build)

Three concrete divergences already surfaced — all present in
`git diff scaffold-baseline..HEAD`. Triage/apply these first:

- [ ] **app-form, no `[build-system]`** → the `project_type: app | lib` work
      (see `2026-06-24-000-...`). _Parameterizable._
- [ ] **`pytest-pyright>=0.0.7` is unresolvable** — only `<=0.0.6` exists on
      PyPI, so the scaffolded dev env can't resolve as shipped. Lower the pin
      (or drop the upper intent). _Upstream-generic — breaks every scaffold._
- [ ] **no CI is scaffolded** — the template's workflows live outside
      `copier-template/`, so generated repos get none. Add a `ci.yml` (strict
      pyright + pytest) and optionally `dependabot.yml`. _Upstream-generic._

## Success Criteria

- [ ] Every hunk in `scaffold-baseline..HEAD` has been triaged (none ignored).
- [ ] Upstream-worthy divergences are reflected in the template.
- [ ] `copier update` round-trips into `basedpyright-as-pyright` cleanly.

## Notes

Depends on `2026-06-24-000-copier-projecttype-app--lib-question.md` — the
`project_type` question is the single biggest expected divergence (app→lib), so
that work and this harvest overlap heavily.
