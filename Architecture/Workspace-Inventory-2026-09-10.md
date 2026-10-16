# Workspace Inventory - 2026-09-10

**Status:** inventory only. No files moved. No files deleted.

## Purpose

This inventory supports future workspace cleanup without risking Grabio code, client data, backups, or reporting evidence.

## High-Level Categories Found

### Main Platform

Path: `/home/anwar/Documents/grabio space`

Contains:

- React/TypeScript platform app.
- Firebase Functions.
- Firebase rules/config.
- Scripts.
- Repo-level docs.
- Reporting evidence.

Risk:

- Root files and folders are build-sensitive. Do not reorganize by folder name alone.

### Mobile Apps

Paths:

- `/home/anwar/Documents/grabio space/grabio-mobile`
- `/home/anwar/Documents/grabio space/grabio-invoice-mobile`

Contains:

- Mobile source code.
- App config.
- Package files.
- Release/build outputs.

Risk:

- Mobile config and release files may be required for Play builds or client testing.

### Embedded / Vendor Finance

Path: `/home/anwar/Documents/grabio space/vendor/beirut-finance-flow-main`

Contains:

- Finance/accounting module source.
- Ledger/reporting/accounting UI code.
- Package files.

Risk:

- This is connected to main Business Finance behavior. Do not move without build and import review.

### Parallel / Backup Structure

Path: `/home/anwar/Documents/grabio space/suba eco sys`

Contains:

- Backup or parallel ecosystem structure.
- Supabase experiment.
- Finance copies.
- POS planning/build packs.
- AI Builder copy.

Risk:

- Looks messy but may contain active reference, backup, or migration knowledge. Do not delete.

### Backups

Path: `/home/anwar/Documents/grabio space/backups`

Contains:

- Migration snapshots.
- Accounting snapshots.
- Post-migration reports.
- Historical restore data.

Risk:

- Backup folders may be the only rollback source.

### Reporting Evidence

Path: `/home/anwar/Documents/grabio space/reporting/data`

Contains:

- JSON audit outputs.
- Import reports.
- Client evidence.
- PDF outputs.

Risk:

- These files are source evidence for data integrity and client-facing numbers.

### Client Data

Known path:

- `/home/anwar/Documents/grabio space/jinan`

Contains:

- Client-specific review docs and generated assets such as QR/PDF files.

Risk:

- Client setup files may be needed for tomorrow or future onboarding.

### Loose / Legacy Docs

Examples found:

- `structure.md`
- `firepayment.md`
- `docs/planning/*`
- `docs/handoff/*`
- `docs/reports/*`
- older module and ecosystem notes.

Risk:

- Some legacy docs may be superseded, but they can contain decision history.

## Inventory Classification Rules

Before any move, classify each file/folder as one of:

- Protected code.
- Protected config.
- Mobile app.
- Embedded/vendor module.
- Backup/restore.
- Client data.
- Reporting evidence.
- Active docs.
- Legacy docs.
- Generated artifact.
- Unknown.

Unknown means do not move.

## Proposed Future Organization

Do not execute this without approval.

- Keep protected code and config in place.
- Keep `reporting/data/` as evidence archive.
- Keep app roots in place.
- Keep vendor roots in place.
- Inventory `suba eco sys/` before deciding whether it is backup, parallel active work, or archive.
- Move only approved loose docs into `docs/`.
- Move only approved client data into a future `client-data/{client}/` structure.
- Move only approved stale files into `_quarantine/YYYY-MM-DD/` with manifest.

## Required Manifest For Any Future Move

Every future move batch needs:

- Original path.
- Proposed path.
- Category.
- Reason.
- Git tracked/untracked status.
- Reference search result.
- Approved by Anwar.
- Move date.
- Restore instruction.

## Current Safety Decision

For 2026-09-10:

- No moves.
- No deletes.
- No quarantine execution.
- Inventory and docs only.
