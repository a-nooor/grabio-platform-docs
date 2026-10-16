# Role, Permission, and Environment Policy

**Last updated:** 2026-09-10

## Purpose

Builder access, accounting access, sub-account roles, permissions, and client work environments must become reusable platform rules. They must not remain one-account setup or hidden account patches.

## Current Status

Owner assessment: about 60% built, but needs more work.

Current code shows:

- Fixed sub-account roles in `src/types/subaccount.ts`.
- Fixed role permission templates in `ROLE_PERMISSIONS`.
- Builder client role: `web_maintenance`.
- Accounting client role: `accounting`.
- Route gates in `src/lib/webBuilderAccess.ts`.
- Builder demo/staging environment separation in `ThemeEditor.tsx`, WordPress provisioning, and builder demo docs.
- Accounting entry paths under `/admin/finance/*` and pairing APIs.

This is a strong start, but it is still mostly code-defined. It is not yet a general tenant-configurable policy system.

## Current Role Model

Known sub-account roles:

- `sales`
- `delivery`
- `manager`
- `cashier`
- `web_maintenance`
- `accounting`

Known route policies:

- Web builder client workspace can access dashboard, theme editor, templates, builder, products, announcements, and blog.
- Accounting freelancer client workspace can access finance, invoice manager, and reports.

## Required Platform Direction

Roles and permissions must be treated as platform policy:

- Default role templates are provided by Grabio.
- Store admins can use defaults without customization.
- Store admins can customize allowed permissions when the package supports it.
- Builder/accounting freelancer environments must be generated from the same role-policy model.
- Web, Functions, mobile, POS, and invoice app must resolve permissions consistently.
- Permissions must be documented and auditable.

## Source Of Truth Target

Target source of truth:

- `storeProfiles/{storeId}.roleSettings` or equivalent store-scoped role policy.
- `subAccounts/{subAccountId}` stores assigned role and any explicit permission overrides.
- Shared resolver returns effective permissions for the user, store, role, package, environment, and surface.

Target resolver:

- `resolveEffectiveRolePolicy(storeId, userId, context)`

The resolver should return:

- Actor type: owner, admin, sub-account, freelancer, builder, accounting, CRM rep, delivery, cashier.
- Store scope.
- Environment scope: production store, demo workspace, staging builder, finance workspace, mobile, POS.
- Allowed routes.
- Allowed data domains.
- Allowed actions.
- Sensitive-field visibility, such as product cost and financial data.
- Reason for deny when blocked.

## Environment Model

Every role must be evaluated inside an environment:

- **Production store:** real client/store data.
- **Builder demo workspace:** staging/demo only; no client domain go-live path.
- **Website builder workspace:** storefront/theme/content/product setup.
- **Accounting workspace:** finance, invoices, reports, GL/accounting setup.
- **Mobile workspace:** role-limited mobile views and actions.
- **POS workspace:** device/store/location-limited actions.

Environment is part of authorization. A user may be allowed in builder demo but blocked from production finance, or allowed in accounting but blocked from website/product-cost editing.

## Current Gaps

1. `ROLE_PERMISSIONS` is fixed in code, not store-configurable.
2. `web_maintenance` and `accounting` roles are special cases, not general role policy templates.
3. Route allowlists are hardcoded in `webBuilderAccess.ts`.
4. No central permission resolver is shared by web, Functions, mobile, POS, and invoice app.
5. No documented `roleSettings` model exists in `storeProfiles`.
6. Environment scope is spread across builder demo logic, route guards, and provisioning services.
7. Permission behavior can drift between main web, mobile, and backend enforcement.
8. Some access is account setup rather than productized admin configuration.

## Non-Negotiable Rules

1. Do not add a one-account role/permission exception unless it is documented as a temporary exception.
2. Do not add new builder/accounting access by only patching a user account.
3. New role behavior must become a default role template or tenant option.
4. Every permission must define read access, write access, route access, sensitive-field access, and environment scope.
5. Mobile and backend enforcement must be considered before a role is marked done.
6. Builder users must not see finance/cost data unless explicitly allowed.
7. Accounting users must not get website/admin powers unless explicitly allowed.
8. Demo/staging environments must not trigger production go-live flows.

## Future-Agent Gate

Before changing roles, permissions, builder access, accounting access, or environment rules, answer:

1. Is this a platform role template or a tenant override?
2. Which package/module enables it?
3. Which environment does it apply to?
4. Which routes are allowed?
5. Which data domains are visible?
6. Which actions are allowed?
7. Which sensitive fields are hidden?
8. Does mobile need the same rule?
9. Does Functions/backend enforce the same rule?
10. Does POS need the same rule?
11. Is there an admin UI for store-level customization?
12. What docs were updated?

If these answers are unclear, stop before coding.

## Immediate Priorities

1. Define `roleSettings` or equivalent tenant role-policy schema.
2. Convert `ROLE_PERMISSIONS` into default role templates.
3. Replace hardcoded route allowlists with role/environment policy resolution.
4. Add admin UI for role customization when package allows it.
5. Sync effective role policy to mobile and backend enforcement.
6. Add audit visibility: who has access to builder, accounting, finance, products, POS, and mobile actions.
