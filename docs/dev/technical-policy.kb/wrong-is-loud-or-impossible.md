---
force: must
why:
  - design/020-goals.kb/uniform-polyglot-model.md
  - design/020-goals.kb/drive-by-friendly.md
---

# Doing it wrong is an error or impossible — never quiet

A wrong outcome **must** be an error or be impossible to express; it **must
not** be the wrong thing done quietly. Concretely, every effectful operation
**must** re-check its own invariants (it _self-guards_) rather than trust the
caller or the orchestration — so no entry point, call order, or UI can drive it
to a wrong result. The guard is co-located with the dangerous action; bypassing
the guard requires bypassing the action.

The read/write vocabulary (`get-require-ensure-verbs.md`) carries the failure
contracts that make this concrete:

- a `get-` that cannot determine its answer **must** error — never emit `""` or
  a default;
- a `require-` **must** treat "pending" and "a required check missing" as
  failure — no vacuous pass;
- an `ensure-` **must** refuse a divergent state (already-present-but-different
  → hard error), never overwrite or silently skip. Re-running toward an
  _identical_ state is a no-op success — that silence is correct; divergent
  silence is the forbidden one.

Non-negotiable: a system whose misuse fails silently cannot be trusted by a
drive-by contributor, and erodes the homogeneity it claims.
