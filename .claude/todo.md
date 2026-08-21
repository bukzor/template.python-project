---
managed-by: Skill(llm-subtask)
cost-benefit-sweh:
  timebox:
    "@value": 2
    rationale:
      "mostly aggregator, plus one remaining scaffold fix (ci.yml) harvested
      from the python-typed-json release; todo.kb children carry their own
      ratings"
    confidence: confident
  benefit-2w:
    "@value": 1
    rationale:
      "unblocks first CI signal for freshly-scaffolded projects; the other
      harvested fixes (unsatisfiable pytest-pyright pin, license mismatch,
      hardcoded pyupgrade target, stale pre-commit-hooks rev, missing PyPI
      metadata) already landed"
    confidence: confident
---

- [ ] Add a `ci.yml` workflow (`.github/` is entirely absent today)
- [ ] [todo.kb/2026-06-24-000-copier-projecttype-app--lib-question.md](todo.kb/2026-06-24-000-copier-projecttype-app--lib-question.md)
      — add `project_type: app | lib` copier question (library compatibility)
- [ ] [todo.kb/2026-06-27-000-harvest-template-improvements-from-basedpyright-as-pyright.md](todo.kb/2026-06-27-000-harvest-template-improvements-from-basedpyright-as-pyright.md)
      — triage `basedpyright-as-pyright` scaffold→final diff into template
      improvements
- [ ] [todo.kb/2026-06-28-000-adopt-buck2-as-the-polyglot-spine-rename--pythonnode-proof.md](todo.kb/2026-06-28-000-adopt-buck2-as-the-polyglot-spine-rename--pythonnode-proof.md)
      — rename + Python+Node buck proof + cell-alias spike + third-party derisk

## Later

We haven't (yet) decided where to place these in the task queue. Please read and
consider slotting them.

- (none)
