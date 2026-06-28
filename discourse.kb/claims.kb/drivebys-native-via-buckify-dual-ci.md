---
status: asserted
likelihood: 0.85
date-observed: 2026-06-24
tags: [drive-by, buckify, ci, contributors]
depends: [definitions.kb/buckify.md, definitions.kb/stutter-step.md]
---

# Drive-by contributors can stay buck-unaware — via buckify + dual-CI equivalence

The real invariant is not "generate BUCK" but **native tools remain a
_sufficient_ build for the contributor loop, and CI proves buck ≡ native**
(every PR runs both; they must agree). Buckify is the mechanism; dual-CI
equivalence is the guarantee.

Three make-or-break properties:

1. generated BUCK is **non-editable** (gitignored or committed read-only — the
   `.templated/ chmod 444` instinct);
2. the native build stays first-class (the failure mode is the repo quietly
   becoming buck-only-buildable);
3. confine buck-only features to paths drive-bys don't touch.

Honest cost: drive-by friendliness is **purchased with maintainer toil** (you
carry the buckify tooling + green dual CI), not eliminated. It is a spectrum:
buck out-of-tree → committed-but-generated/read-only → hand-authored-primary,
with friendliness falling and buck-power rising left-to-right.

Answers `questions.kb/keep-drivebys-buck-unaware.md`.
