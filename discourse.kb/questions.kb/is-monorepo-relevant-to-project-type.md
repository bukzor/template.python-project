---
resolved: claims.kb/monorepo-orthogonal-to-project-type.md
sources: [sources.kb/design-chat-2026-06.md]
tags: [project_type, monorepo, copier]
---

# Is monorepo structure relevant to the project_type: app|lib task?

The originating question. Resolved: **yes, but as an orthogonal substrate, not
part of `project_type`** (claims.kb/monorepo-orthogonal-to-project-type.md).
app-vs-lib is the root package shape; workspace/multi-package is an independent
axis beneath both. Reframes `project_type` to "where the primary package lands."
