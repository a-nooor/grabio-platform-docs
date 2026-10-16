# Workspace Organization Policy

**Last updated:** 2026-09-10

## Purpose

Grabio workspace organization must protect data first. The workspace contains main platform code, mobile apps, invoice apps, vendor copies, backup structures, client data, reporting evidence, scripts, and planning docs. Future agents must not move or delete files casually.

## Memory Rule

Every important planning decision from the engineering conversation must be documented before moving to implementation. Do not rely on chat memory alone.

Document at least:

- Architecture decisions.
- Workspace structure decisions.
- Client-specific setup discoveries.
- Tenant option rules.
- UI-first setup rules.
- ERP maturity gaps.
- Quarantine and deletion policies.
- Any approved file move plan.

Use the canonical docs vault as the source of truth, then mirror short pointers in the repo docs where needed.

## Protected Code Roots

Do not move these folders without a separate refactor plan, build-impact review, and Anwar approval:

- `/home/anwar/Documents/grabio space/src`
- `/home/anwar/Documents/grabio space/functions`
- `/home/anwar/Documents/grabio space/public`
- `/home/anwar/Documents/grabio space/grabio-mobile`
- `/home/anwar/Documents/grabio space/grabio-invoice-mobile`
- `/home/anwar/Documents/grabio space/vendor`
- `/home/anwar/Documents/grabio space/white-label-client-app`
- `/home/anwar/Documents/grabio space/suba eco sys`

Reason: these paths may be used by builds, imports, docs, scripts, mobile packaging, deployment, or historical restore work.

## Recommended Workspace Zones

Use this structure for future organization planning:

- **Main platform:** root app, `src/`, `functions/`, Firebase config, deployment config.
- **Apps:** `grabio-mobile/`, `grabio-invoice-mobile/`, `white-label-client-app/`.
- **Vendor / embedded modules:** `vendor/`.
- **Backup or copied structures:** `suba eco sys/`, `backups/`, legacy local copies.
- **Docs:** `docs/` in repo plus canonical docs vault.
- **Client data:** client-specific folders such as `jinan/`, source sheets, PDFs, imports, and setup evidence.
- **Reporting evidence:** `reporting/data/` and `reporting/assets/`.
- **Scripts:** `scripts/`, with outputs written to `reporting/data/` when used as evidence.
- **Quarantine:** `_quarantine/YYYY-MM-DD/` only after approval.

## Inventory Before Moves

Before moving any file or folder:

1. Create an inventory report.
2. Classify each item as code, docs, client data, report evidence, backup, generated artifact, credential-sensitive, or unknown.
3. Identify whether the file is tracked by git.
4. Search for references to the original path.
5. Produce a proposed move list.
6. Wait for Anwar approval.

No bulk move is allowed without the inventory and proposed move list.

## Quarantine Policy

Quarantine is for files that are probably stale, duplicate, temporary, misplaced, or no longer needed, but are not safe to delete immediately.

Required quarantine folder format:

- `_quarantine/YYYY-MM-DD/docs/`
- `_quarantine/YYYY-MM-DD/client-data/`
- `_quarantine/YYYY-MM-DD/backups/`
- `_quarantine/YYYY-MM-DD/generated/`
- `_quarantine/YYYY-MM-DD/unknown/`

Every quarantine batch must include:

- `_quarantine/YYYY-MM-DD/MANIFEST.md`

The manifest must include:

- Original path.
- New quarantine path.
- Reason for quarantine.
- Moved by.
- Move date.
- Review date, normally move date plus 40 days.
- Delete approval status.
- Restore notes.

## Deletion Rule

No automatic deletion.

After 40 days, quarantined files may be reviewed for deletion, but deletion still requires explicit approval from Anwar in that future session.

Future agents must not interpret "40 days" as permission to delete. It means "eligible for review."

## Safe Move Procedure

1. Snapshot `git status`.
2. Create inventory report.
3. Prepare proposed move list.
4. Ask for approval.
5. Move only approved paths.
6. Write or update quarantine manifest.
7. Re-run `git status`.
8. Search for broken path references.
9. Report moved paths and any unresolved risk.

## Never Move Without Approval

- `.credentials.md`
- `.env*`
- Firebase credentials or mobile config files.
- Build config files.
- Source folders.
- Release artifacts.
- Reporting evidence used for client numbers.
- Backup folders that may be the only restore point.
- Unknown files.

## Current Workspace Observation

Read-only scan on 2026-09-10 showed mixed categories in the workspace:

- Main platform code and Functions.
- Mobile apps and invoice mobile app.
- Vendor finance module.
- `suba eco sys/` backup or parallel structure.
- `backups/` migration snapshots.
- `reporting/data/` evidence JSON/PDF files.
- `jinan/` client data.
- Many planning, handoff, report, and legacy Markdown files.

The workspace should be organized by inventory and approved move list, not by blind cleanup.
