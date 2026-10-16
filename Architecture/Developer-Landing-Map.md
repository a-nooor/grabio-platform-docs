# Developer Landing Map

**Last updated:** 2026-09-10

## Purpose

This is the first map a developer or agent should read before working in the Grabio workspace.

Goal: understand the project structure in under 5 minutes without guessing, moving files, or treating old backup folders as active code.

## Read First

1. `/home/anwar/Documents/grabio space/README.md`
2. `/home/anwar/Documents/grabio space/architecture.md`
3. `/home/anwar/Documents/grabio space/decision-log.md`
4. `/home/anwar/Documents/grabio-platform-docs/Architecture/Packages-Workflows-Modules.md`
5. `/home/anwar/Documents/grabio-platform-docs/Architecture/Fine-Dining-Platform-Map.md`
6. `/home/anwar/Documents/grabio-platform-docs/Architecture/Workspace-Organization-Policy.md`
7. `/home/anwar/Documents/grabio-platform-docs/Architecture/Setup-Surface-Separation.md`
8. `/home/anwar/Documents/grabio-platform-docs/Architecture/Role-Permission-Environment-Policy.md`
9. `/home/anwar/Documents/grabio-platform-docs/Architecture/Resolver-Contracts.md`

## Workspace Zones

### Main Platform

Path: `/home/anwar/Documents/grabio space`

Purpose: production Grabio web/admin platform, Firebase Hosting, Firebase Functions, Firestore rules, scripts, reports, and docs.

Important roots:

- `src/` - React/TypeScript web/admin/public app.
- `functions/` - Firebase Cloud Functions API, triggers, scheduled jobs.
- `public/` - static assets and public files.
- `firebase.json`, `firestore.rules`, `firestore.indexes.json`, `storage.rules` - deployment/runtime config.
- `scripts/` - Admin SDK setup, audit, sync, and backfill scripts.
- `reporting/data/` - evidence outputs used for audits and client-safe numbers.
- `docs/` - repo-local planning, handoff, deployment, and report docs.

### Mobile Admin App

Path: `/home/anwar/Documents/grabio space/grabio-mobile`

Purpose: Grabio mobile app for owner/admin/team/customer flows.

Risk: mobile often needs the same tenant settings and role rules as web. Do not add web-only settings without checking mobile impact.

### Invoice Mobile App

Path: `/home/anwar/Documents/grabio space/grabio-invoice-mobile`

Purpose: standalone invoice/finance mobile app.

Risk: invoice template, finance roles, reminders, and PDF/document behavior can drift from main web finance unless documented.

### Embedded / Vendor Finance

Path: `/home/anwar/Documents/grabio space/vendor/beirut-finance-flow-main`

Purpose: finance/accounting module source embedded into the main platform.

Risk: changes here may affect Business Finance screens, GL, vouchers, reports, PDFs, and invoice manager behavior.

### POS / Ecosystem / Parallel Structures

Path: `/home/anwar/Documents/grabio space/suba eco sys`

Purpose: backup or parallel ecosystem structure containing older copies, POS planning, finance copies, AI builder, and Supabase experiments.

Risk: do not assume this is active production code. Do not delete or move it without inventory and approval.

### Client Data

Examples:

- `/home/anwar/Documents/grabio space/jinan`
- client-specific PDFs, Excel exports, import files, setup notes, and review docs.

Rule: client data must be classified before moving. It may be active evidence for tomorrow or future client work.

### Reporting Evidence

Path: `/home/anwar/Documents/grabio space/reporting/data`

Purpose: proof files for audits, syncs, imports, closures, and client-safe data.

Rule: never delete, move, or rewrite evidence casually. Client-facing numbers must trace to files here.

### Backups

Path: `/home/anwar/Documents/grabio space/backups`

Purpose: migration snapshots, rollback exports, and historical restore points.

Rule: backups may look messy but can be the only restore source. Quarantine only after inventory and approval.

## Active Architecture Maps

- `Packages-Workflows-Modules.md` - package, workflow, module, tenant option, and ERP maturity map.
- `Fine-Dining-Platform-Map.md` - active product pivot: fine-dining operations plus CRM, with accounting/inventory optional and broad verticals deferred.
- `Workspace-Organization-Policy.md` - safe cleanup, quarantine, protected roots, no-delete policy.
- `Setup-Surface-Separation.md` - Store Profile vs Invoice Document vs Website Template ownership.
- `Role-Permission-Environment-Policy.md` - builder/accounting roles, permissions, and environments.
- `Resolver-Contracts.md` - future shared resolver contracts.

## Work Method For Future Agents

Before code:

1. Read the relevant architecture map.
2. Classify the work: global fix, tenant option, account data setup, or temporary exception.
3. Identify all surfaces: web, Functions, mobile, POS, invoice app, scripts.
4. Check whether the change affects tomorrow/client-critical data.
5. Update docs before implementation.

Before moving files:

1. Read `Workspace-Organization-Policy.md`.
2. Create inventory.
3. Create proposed move list.
4. Wait for Anwar approval.
5. No deletion without explicit future approval.

Before setup work:

1. Ensure backend setup is visible in UI.
2. Ensure user can review, correct, and continue from UI.
3. Write evidence to `reporting/data/` when client data or numbers are involved.

## Today Safety Status

For 2026-09-10, before the critical client accounting setup on 2026-09-11:

- Docs and plans only.
- No deploy.
- No migration.
- No file movement.
- No production data change.
- No risky accounting/POS/mobile/invoice refactor.

## Current Critical Platform Backlog - 2026-09-14

Source: `/home/anwar/Documents/grabio space/reporting/data/platform-pos-discovered-fixes-2026-09-14.md`

Priority order:

1. P0 mobile Play manager/store-admin parity and committed tenant binding, Play versionCode 140 or higher, no client sideload.
2. P1 platform tenant/role cleanup: duplicate manager email risk, web `role === 'admin'` audit, Little Hands expense tiles, subscription owner-only documentation.
3. P1 mobile owner-only leftovers: CRM map, sales order policy, create order branches, profile sub-account load order.
4. P2 POS RBAC boundary: Windows POS local cashier/manager/admin roles are not Firebase sub-account roles unless a staff-aware POS design is approved.

Rule: these are platform fixes discovered from client setup, not one-account patches.

## Product Pivot - 2026-09-15

Grabio's active product direction is now fine-dining restaurant daily operations plus CRM.

Future agents must treat:

- Restaurant/fine dining and CRM as the active growth core.
- Accounting, finance, inventory, recipes, costing, and purchasing as optional maturity modules for restaurants.
- Builder, template, SEO, and content as connected high-end client modules inside Grabio, not a separate platform.
- Shop, manufacturing, and existing builder clients as maintenance/support areas.
- NGO, freelancer, mini shop, publisher, and broad custom verticals as deferred unless Anwar explicitly reopens them.

Before building new restaurant features, review the real client workflow draft or Excel source and classify each request as daily operation, CRM, tenant option, report, automation, role/security, setup/import, optional inventory, optional finance, or temporary exception.
