---
resolved: claims.kb/drivebys-native-via-buckify-dual-ci.md
sources: [sources.kb/design-chat-2026-06.md]
tags: [drive-by, contributors, buckify]
---

# Can buck adoption avoid hurting drive-by contributions?

Resolved **yes, conditionally**
(claims.kb/drivebys-native-via-buckify-dual-ci.md): buckify generates BUCK from
native configs and CI proves buck ≡ native, so drive-bys stay on native tools.
Holds only while generated BUCK is non-editable, the native build stays
sufficient, and buck-only features are confined to maintainer paths. Cost is
shifted to maintainer toil, not eliminated.
