---
title: Client requests become tenant options by default
date: 2026-09-10
repos: grabio.space, ecosystem.git
---

# 2026-09-10 — Client requests become tenant options by default

**Context:** Recent Grabio work spans the main platform, POS, mobile apps, and new-client data setup. Client discoveries such as Jinan's Kitchen reservations/advance orders, NIPCO order-status preferences, configurable sub-account roles, and payment-method availability exposed the risk of turning tenant needs into hidden shared-code patches. Data setup also exposed a product gap: backend scripts and AI setup are useful starters, but store owners need UI paths to see, correct, and continue the setup.

**Decision:** Treat Grabio as a configurable multi-tenant platform. A client-specific request must be classified before implementation as a global platform fix, tenant option, account data setup, or temporary exception. If different stores can reasonably need different behavior, implement it as a tenant option with safe defaults and admin control, then make web, POS, mobile, and Functions read the same effective setting. Store setup must be UI-first: scripts/imports/AI agents can prepare data, but every setup result must be visible, reviewable, editable where allowed, and connected to the next admin UI step.

**Rejected alternatives:**

- Per-client hardcoded branches — fast short-term, but creates untestable behavior drift across accounts.
- Editing only the affected account without a platform model — acceptable only for pure data setup, not workflow or UX behavior.
- Letting mobile/POS duplicate settings separately — causes checkout, order, and payment mismatches.
- Treating backend data setup as final delivery — hides setup knowledge from the client and prevents the platform from becoming smarter.

**Consequences:** Future agents must document the classification before code changes, update the settings architecture when adding options, and include cross-surface verification. Existing custom changes should be audited and moved into typed tenant settings where needed. Repeated setup work should produce UI improvements such as Excel template downloads, upload/preview flows, validation messages, AI mapping/correction, approval gates, and links to the configured admin screens.

**Repos affected:** grabio.space | ecosystem.git

**Links:** [[Backlog/Open]], [[Architecture/Packages-Workflows-Modules]]
