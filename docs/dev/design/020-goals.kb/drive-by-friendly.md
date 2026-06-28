---
why:
  - 010-mission.kb/polyglot-self-similar-template.md
---

# Goal: drive-by friendly

A casual community contributor can build, test, and contribute to any generated
repo using **only native ecosystem tools** (uv / pnpm / cargo), without learning
buck or any bespoke tooling, and without their custom work being clobbered by
template updates.

This is the welcoming half of the architecture: low barrier to a first useful
change. It is the goal most policies trade against — it is why buck stays behind
native tools and why cross-repo coupling goes through published artifacts rather
than shared build machinery.
