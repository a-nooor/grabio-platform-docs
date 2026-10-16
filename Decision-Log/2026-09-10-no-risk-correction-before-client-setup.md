---
title: No-risk correction before client accounting setup
date: 2026-09-10
repos: grabio.space, grabio-platform-docs
---

# 2026-09-10 - No-risk correction before client accounting setup

**Context:** Tomorrow has a critical old-client accounting setup with the client's accounting manager. The client may decide whether to stay with Grabio. Today must improve structure and documentation without risking production behavior.

**Decision:** Today is docs/plans only. No deploy, no migration, no production data change, no workspace move, no broad refactor, no POS/mobile/accounting/invoice behavior change. Structural correction work must become documented future PR slices.

**Priorities:**

1. Clean documentation mapping so any developer can understand the workspace quickly.
2. Define the correct infrastructure base without implementing risky changes.
3. Build a sustainable working method where follow-up fixes upgrade the structure.

**Consequences:** Future structural implementation waits until after the client setup or explicit owner approval. Tomorrow's work must use stable UI/script paths only and document any product gaps as follow-up.

**Repos affected:** grabio.space | grabio-platform-docs

**Links:** [[Architecture/Developer-Landing-Map]], [[Backlog/Structural-PR-Slices]], [[Runbooks/Client-Accounting-Setup-No-Risk]]
