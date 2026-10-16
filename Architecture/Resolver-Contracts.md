# Resolver Contracts

**Last updated:** 2026-09-10

## Purpose

Grabio needs shared resolver contracts before more business types, tenant options, roles, apps, and setup flows are added.

Today this is documentation only. Do not implement these contracts before a separate approved coding plan.

## Why Resolvers Matter

Current risk:

- Web, Functions, mobile, invoice app, and POS can read different slices of store settings.
- Package/module logic can drift between `src/` and `functions/`.
- Role/permission behavior can be correct in web but missing in mobile or backend.
- Setup scripts can create data that the UI cannot continue.

Target:

- One effective answer per store/user/context.
- Same behavior across all surfaces.
- Explicit defaults for old stores.
- Clear source-of-truth and fallback order.

## Resolver 1: Store Settings

Name:

- `resolveEffectiveStoreSettings`

Inputs:

- `storeId`
- `StoreProfile`
- optional environment context: web, marketplace, Functions, mobile, POS, invoice app

Returns:

- Store identity settings.
- Order settings.
- Payment settings.
- Reservation and advance-order settings.
- Inventory settings.
- Setup progress.
- UI visibility rules.
- Fallback metadata showing which value came from default, store profile, tenant option, or compatibility field.

Must answer:

- Which settings are enabled?
- Which settings are visible to the user?
- Which settings are editable?
- Which settings are package-gated?
- Which settings are defaulted for old stores?

## Resolver 2: Role Policy

Name:

- `resolveEffectiveRolePolicy`

Inputs:

- `storeId`
- `userId`
- user role
- sub-account role
- package/modules
- environment context
- route/action/data domain

Returns:

- Actor type.
- Environment scope.
- Allowed routes.
- Allowed actions.
- Allowed data domains.
- Sensitive-field visibility.
- Mobile/POS permissions.
- Backend enforcement decision.
- Deny reason.

Must answer:

- Can this user enter this workspace?
- Can this user read this data?
- Can this user write this data?
- Can this user see cost, finance, accounting, customer, POS, or setup data?
- Is this production, staging/demo, finance, mobile, or POS scope?

## Resolver 3: Module Capabilities

Name:

- `resolveEffectiveModuleCapabilities`

Inputs:

- `StoreProfile`
- `StartingPackageKey`
- `BusinessWorkflow`
- `enabledModules`
- subscription status
- package gates

Returns:

- Enabled modules.
- Locked modules.
- Package defaults.
- Add-ons.
- Mutually exclusive modules.
- Workflow-specific requirements.
- Migration/version state.

Must answer:

- Which modules are active?
- Which are available but off?
- Which are unavailable because of package?
- Which are mutually exclusive?
- Which surfaces should show/hide the module?

## Resolver 4: Setup Progress

Name:

- `resolveSetupProgress`

Inputs:

- `storeId`
- store profile
- products/materials/recipes/payment/roles/template state
- package/workflow

Returns:

- Required setup steps.
- Completed setup steps.
- Blocked setup steps.
- Missing data.
- Suggested UI action.
- Whether setup came from manual UI, import, AI setup, script, or migration.

Must answer:

- What does the store need next?
- Where should the user continue in UI?
- Which data was backend-created and needs UI confirmation?
- Which setup can be skipped because package/workflow does not need it?

## Shared Rules

1. Resolvers must be pure where possible.
2. Defaults must be explicit.
3. Compatibility fields must be labelled as compatibility, not new source of truth.
4. Every consuming surface must be listed before implementation.
5. Mobile and Functions cannot be afterthoughts.
6. No client-specific hardcoded store IDs for normal behavior.
7. Resolver changes require docs and verification.

## Implementation Later, Not Today

Future coding should happen in small slices:

1. Define types only.
2. Add tests for defaults.
3. Wire web read paths.
4. Wire Functions read paths.
5. Wire mobile read paths.
6. Wire POS contract.
7. Add admin UI where settings are editable.

No resolver code should be added on 2026-09-10 because tomorrow has a critical client accounting setup.
