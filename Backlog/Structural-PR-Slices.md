# Structural PR Slices

**Last updated:** 2026-09-14

## Purpose

These are future safe implementation slices. Do not bundle them into one large refactor.

No structural PR should be started before tomorrow's client accounting setup unless Anwar explicitly approves.

## Urgent Discovered Fixes - 2026-09-14

Source: `/home/anwar/Documents/grabio space/reporting/data/platform-pos-discovered-fixes-2026-09-14.md`

These items were discovered during production data migration/client setup work. They must be treated as platform improvements, not one-account patches.

### P0: Mobile Play Manager Parity

Goal:

- Ship `grabio-mobile` Play release where manager sub-accounts behave as store admins for back-office modules, matching web behavior.

Scope:

- Use `hasStoreAdminAccess` / manager parity, not owner-only gates.
- Include committed tenant binding and mismatch guard work.
- Release through Google Play only, versionCode 140 or higher.
- No client sideload.

Done when:

- Little Hands manager verifies from Play build.
- Tenant binding evidence is updated.
- No manager is bound to the wrong store.

Risk:

- High client-facing priority. Do before lower-priority cleanup.

### P1: Tenant Binding and Web Admin Role Audit

Goal:

- Remove account-specific manager fixes and make tenant/role behavior consistent.

Scope:

- Resolve duplicate `manager@` sub-account email across Little Hands and NIPCO.
- Keep binding order: `users.subAccountId` first, then that `subAccounts.storeId`.
- Audit web admin routes still using `user.role === 'admin'`.
- Replace suitable checks with store-admin-aware helpers.
- Document subscription/billing as owner-only where intended.

Done when:

- No unscoped `limit(1)` email lookup can bind manager to the wrong tenant.
- Store admin helpers are used where manager should behave as admin.
- Billing/subscription owner-only behavior is explicit in UI/docs.

Risk:

- High. Tenant isolation issue is Sev-1 if wrong store data appears.

### P1: Mobile Store Admin Leftovers

Goal:

- Audit owner-only leftovers in mobile after the Play release.

Scope:

- CRM team map owner-only checks.
- Sales order policy owner-only checks.
- Create order owner-only branches.
- Profile sub-account load order: prefer `subAccountId` before email lookup.

Done when:

- Mobile manager parity matches web for approved back-office surfaces.
- Mobile tenant resolution follows the same binding order as web.

Risk:

- Medium/high because mobile release cycle is slower than web.

### P2: POS RBAC Boundary

Goal:

- Clarify Windows POS local roles vs Firebase sub-account roles.

Scope:

- Document that POS local `cashier`, `manager`, and `admin` are not the same as Firebase `subAccounts`.
- Confirm pairing is store/device scoped, not per-staff Firebase login.
- Decide whether platform role should map into POS role at pair time or stay separate.
- Retest V.POS/mobile POS after Play manager fix.

Done when:

- POS RBAC decision is documented in the POS sync contract.
- Little Hands POS expectations are clear before POS UAT.

Risk:

- Medium. Do not mix POS local staff login with Firebase tenant auth without a design.

## Slice 1: Developer Landing Map Pointers

Goal:

- Make repo entry points point to the canonical developer landing map.

Scope:

- Docs only.
- No code.
- No data.

Done when:

- `README.md` and `architecture.md` point to `Developer-Landing-Map.md`.

## Slice 2: Manifest Sync Check

Goal:

- Prevent `src/lib/moduleManifest.ts` and `functions/src/lib/moduleManifest.ts` from drifting.

Scope:

- Add read-only comparison script.
- Add test/check command.
- No behavior change.

Done when:

- CI/local check fails if package keys, workflows, or module defaults differ.

Risk:

- Low if check-only.

## Slice 3: Store Settings Resolver Types

Goal:

- Define `resolveEffectiveStoreSettings` types and defaults.

Scope:

- Types and tests first.
- No UI behavior change.
- No Firestore migration.

Done when:

- Existing stores resolve stable defaults.
- Tests cover missing settings.

Risk:

- Medium if wired into UI too early. Keep type/test-only first.

## Slice 4: Role Policy Schema

Goal:

- Convert fixed `ROLE_PERMISSIONS` into default role templates and prepare `roleSettings`.

Scope:

- Types and documentation.
- Preserve current permissions exactly.
- No admin UI yet.

Done when:

- Existing sales, delivery, manager, cashier, web builder, and accounting roles resolve the same permissions through the new model.

Risk:

- Medium. Must not break builder/accounting access before client work.

## Slice 5: Setup Surface Ownership Cleanup

Goal:

- Clarify Store Profile, Invoice Document setup, and Website Template ownership.

Scope:

- Decide invoice numbering owner.
- Clarify `AdminTemplates.tsx` vs `ThemeEditor.tsx`.
- Add links between pages.

Done when:

- No page silently writes another surface's owned fields.
- Invoice numbering decision is documented and implemented.

Risk:

- Medium/high because invoice templates and NIPCO lock are sensitive.

## Slice 6: Backend-Only Setup UI Visibility

Goal:

- Ensure script/import/AI-created setup is visible and continuable in UI.

Scope:

- Start with one low-risk setup area.
- Show status and links to relevant admin screens.
- No bulk migration.

Done when:

- A user can see what was created, what is missing, and where to continue.

Risk:

- Medium if tied to live client setup. Use read-only/status first.

## Slice 7: Order Status Tenant Option

Goal:

- Replace NIPCO-style hardcoded order-status behavior with tenant settings.

Scope:

- Document settings shape.
- Add defaults.
- Preserve current NIPCO behavior.
- Then wire web/mobile/Functions.

Done when:

- Store-specific statuses are configurable without hardcoded store IDs.

Risk:

- High. Must not change tomorrow's client behavior.

## Slice 8: Mobile Settings Expansion

Goal:

- Expand mobile store profile sync to include only approved tenant options.

Scope:

- Add typed fields gradually.
- Preserve current mobile behavior.
- Add fallback defaults.

Done when:

- Mobile sees the same effective settings as web for selected fields.

Risk:

- Medium because mobile releases have versioning and Play Store impact.

## Slice 9: Inventory Valuation Ledger Design

Goal:

- Design double-entry stock movement and accounting valuation flow.

Scope:

- Architecture doc first.
- No coding.
- No data migration.

Done when:

- Receipt, sale, return, transfer, adjustment, production consume, and production output events are mapped to stock and GL impact.

Risk:

- High. Must be planned with accounting data protection.

## Slice 10: Automation Hook Model

Goal:

- Define formal domain events and module hooks.

Scope:

- Docs/types first.
- No trigger rewrites.

Done when:

- Order, payment, stock, recipe, customer, invoice overdue, and setup events have documented payloads and subscribers.

Risk:

- Medium/high if existing Cloud Functions are changed too early.
