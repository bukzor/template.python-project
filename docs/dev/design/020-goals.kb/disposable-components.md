---
why:
  - ../010-mission.kb/polyglot-self-similar-template.md
---

# Goal: disposable components

A component can be created, abandoned, or deleted **cheaply and cleanly**, with
its own separate, deletable, quarantine-able history. A throwaway experiment or
a leaked secret in one component is excised by deleting its repo — never by
rewriting a shared monorepo history that everyone else depends on.

This is the disposable half of the architecture, and the decisive reason to
prefer a polyrepo with per-component histories over a single shared history
(e.g. a josh-projected monorepo). It pairs with `drive-by-friendly`: low cost to
start, low cost to walk away.
