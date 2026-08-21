---
force: should
why:
  - design/020-goals.kb/drive-by-friendly.md
  - design/020-goals.kb/disposable-components.md
---

# Punt with a tripwire (auto-YAGNI)

Premature generalization **should** be deferred — but a deferral **must** leave
a tripwire. You **may** special-case the present (one provider, a hardcoded
assumption) only if the special-casing **fails loudly** the moment its
assumption breaks. A silent special-case is prohibited; a loud one is
encouraged.

The payoff is empirical YAGNI: if the tripwire never fires, the generalization
was never needed and was correctly skipped; if it fires, it points exactly at
the work now due — located and obvious. Generalization is paid for by evidence,
not by guesswork.

Instantiations: the single `providers/github/` slot guarded by the no-leak check
(`platform-isolated-in-providers.md`); the `lib/dev/` domain split deferred
until a directory is crowded enough that the grouping is obvious.
