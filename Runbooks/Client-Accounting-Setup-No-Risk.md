# Client Accounting Setup - No-Risk Runbook

**Last updated:** 2026-09-10

## Purpose

Use this runbook for tomorrow's old-client accounting setup with the accounting manager.

Goal: protect the ecosystem and keep the client setup stable. Do not use the meeting as a place to test risky structural changes.

## Before The Meeting

1. Read the client-specific README/handoff if one exists.
2. Confirm the correct store/account identity.
3. Confirm the current accounting mode.
4. Confirm which setup data will be entered or imported.
5. Confirm which UI screen the accounting manager will see.
6. Prepare screenshots or screen path notes if needed.
7. Do not deploy new production code before the meeting.

## Stable Paths Only

Use existing stable UI and script paths only.

Allowed:

- Existing Store Profile fields.
- Existing Business Finance screens.
- Existing Chart of Accounts/accounting setup flow.
- Existing voucher/report screens.
- Existing import/setup scripts only if already used and understood.
- Existing reporting/data evidence outputs.

Not allowed without separate approval:

- Refactoring accounting code.
- Moving invoice numbering.
- Changing invoice template ownership.
- Changing role permissions.
- Changing POS or mobile behavior.
- Changing module manifests.
- Running bulk cleanup.
- Moving workspace folders.
- Deploying production changes.

## During The Setup

1. Keep one source-of-truth note for what the accounting manager requests.
2. If a request is pure data setup, use existing UI or approved script.
3. If a request is a feature/change, classify it:
   - Global platform fix.
   - Tenant option.
   - Account data setup.
   - Temporary exception.
4. Do not implement new behavior during the meeting.
5. If the setup exposes a product gap, document it as follow-up.
6. If data is imported or generated, write evidence under `reporting/data/`.
7. Keep screenshots/display proof separate from closure proof.

## Stop Conditions

Stop and document before continuing if:

- Store/account identity is unclear.
- Accounting mode is unclear.
- A data import would overwrite existing accounting data.
- A script needs `--write` and has not been reviewed.
- The accounting manager requests behavior not supported by current UI.
- A change touches NIPCO-like template locks or production-sensitive templates.
- A fix requires deploy, migration, or broad refactor.

## After The Setup

Document:

- Problem.
- Method.
- Results.
- Evidence files.
- Client-visible UI path.
- Remaining gaps.
- Next steps.

Do not say setup is verified unless the data path was checked through the relevant UI/reporting screen.

## Follow-Up Classification

After the meeting, each new request must become one of:

- Small data setup task.
- Tenant option.
- UI setup improvement.
- Accounting engine fix.
- Report/display fix.
- Role/permission improvement.
- Deferred structural PR.

## Tomorrow Success Criteria

- Client/accounting manager can see the setup in UI.
- No risky production behavior changes were made.
- Any missing platform capability is documented, not improvised.
- Evidence exists for any imported or corrected data.
- Follow-up tasks are structured and safe.
