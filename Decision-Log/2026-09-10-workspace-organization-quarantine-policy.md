---
title: Workspace organization and quarantine policy
date: 2026-09-10
repos: grabio.space, grabio-platform-docs
---

# 2026-09-10 - Workspace organization and quarantine policy

**Context:** The Grabio workspace contains main platform code, POS/mobile/invoice apps, backup structures, client data, reporting evidence, scripts, and planning docs. Random files and folders increase risk for future agents, but blind cleanup risks data loss.

**Decision:** Organize by inventory first. No file or folder should be moved until an inventory report, classification, reference check, and proposed move list are reviewed. Quarantine may be used for uncertain files, but 40 days means eligible for review only, not automatic deletion.

**Rejected alternatives:**

- Blind cleanup by folder name - too risky because backups, client data, and build paths may look random.
- Automatic deletion after 40 days - unsafe because the file may still be the only source of evidence or restore data.
- Moving source/app folders into a new layout without a refactor plan - can break imports, builds, deployment scripts, and mobile packaging.

**Consequences:** Future agents must preserve memory in docs, use the workspace policy before moves, write quarantine manifests, and request explicit approval before any deletion.

**Repos affected:** grabio.space | grabio-platform-docs

**Links:** [[Architecture/Workspace-Organization-Policy]], [[Backlog/Open]]
