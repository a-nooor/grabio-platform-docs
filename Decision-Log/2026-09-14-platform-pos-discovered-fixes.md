---
title: Platform and POS discovered fixes from data migration
date: 2026-09-14
repos: grabio.space, grabio-mobile, POS, grabio-platform-docs
---

# 2026-09-14 - Platform and POS discovered fixes from data migration

**Context:** During production data setup/migration, manager mobile access and POS role assumptions exposed platform gaps. These are platform/structure issues, not one-client setup tasks.

**Decision:** Add discovered fixes to the structural correction plan with priority order:

1. **P0:** Ship Grabio mobile Play release versionCode 140 or higher with manager/store-admin parity and committed tenant binding. No client sideload.
2. **P1 platform:** Fix duplicate manager email risk across Little Hands and NIPCO, audit web `role === 'admin'` checks, keep subscription owner-only by design, and verify Little Hands expense tiles in Stock & Catalog.
3. **P1 mobile:** Audit owner-only leftovers in CRM map, sales order policy, create order branches, and profile sub-account load order.
4. **P2 POS:** Keep Windows POS local cashier/manager/admin separate from Firebase sub-account manager unless a staff-aware POS design is approved.

**Rejected alternatives:**

- Treating manager mobile as only one account setup - wrong because web/mobile role parity is platform behavior.
- Sideloading a client APK - unsafe and not scalable; Play update is required.
- Mixing POS local staff roles with Firebase sub-accounts without design - risks auth confusion and tenant leakage.

**Consequences:** The mobile Play fix is first. Platform/mobile/POS follow-ups must become small PRs after P0, using tenant isolation rules and the role policy. Every fix must write evidence under `reporting/data/` when it changes tenant binding, access, or client-visible behavior.

**Repos affected:** grabio.space | grabio-mobile | POS | grabio-platform-docs

**Links:** [[Backlog/Open]], [[Backlog/Structural-PR-Slices]], `/home/anwar/Documents/grabio space/reporting/data/platform-pos-discovered-fixes-2026-09-14.md`
