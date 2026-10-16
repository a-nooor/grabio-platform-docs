# Fine-Dining Platform Map

**Last updated:** 2026-09-15

## Purpose

Grabio's product center is now fine-dining restaurant daily operations plus a best-in-class, user-friendly CRM.

Accounting, inventory, finance, manufacturing, shop, and builder capabilities are not deleted. They are reclassified so the platform stays focused and does not spread engineering across too many verticals.

## Product Position

Grabio should be built and sold first as:

- Fine-dining restaurant operations management.
- Guest CRM and relationship intelligence.
- Reservation, service, order, staff, and daily management workspace.
- Optional finance, accounting, inventory, costing, purchasing, and reporting expansion when the restaurant is ready.
- Connected website, template, SEO, and content tools for high-end clients, not a separate public builder platform.

Grabio should not continue expanding as a broad generic ERP for every business type.

## Active Product Core

### Restaurant Daily Operations

Owns the daily work of a restaurant:

- Reservations and booking flow.
- Guest arrival and table/service context.
- Orders and kitchen/service status.
- Staff presence and shift activity.
- Daily notes, incidents, requests, and follow-ups.
- Service-line tracking for events, entrance, bar, birthday, private dining, and similar fine-dining operations.
- Daily operational reports.

### Guest CRM

Owns guest memory and relationship quality:

- Guest profile and visit history.
- Preferences, allergies, important dates, VIP notes, and complaints.
- Communication and follow-up tasks.
- Sales/opportunity pipeline where relevant.
- Event and private dining relationship tracking.
- Segmentation and retention actions.

CRM is not a side module. It is part of the restaurant operating system.

### Restaurant Setup

New restaurants can start without accounting or inventory.

Minimum start:

- Store profile.
- Restaurant operating settings.
- Users and roles.
- Reservation/service settings.
- CRM guest fields and follow-up policy.
- Daily operation screens.

Optional later:

- Inventory.
- Recipes and costing.
- Purchasing.
- Accounting.
- Finance reports.
- Payroll and staff cost reporting.
- Multi-branch and warehouse controls.

## Connected High-End Client Modules

Builder, template, and SEO stay connected to Grabio because they share the same tenant, store profile, domain, menu/products, CRM, reservations, and content data.

They should become high-end managed modules, not a separate platform now.

### Website Builder / Template

Status:

- Connected module inside Grabio.
- Used for active clients and high-end restaurant presentation.
- Not pushed as a standalone builder product.

Rules:

- Same store profile and tenant identity.
- Same domain and branding source.
- Separate builder/content roles through role policy.
- No production go-live flow from demo/staging without explicit approval.

### SEO / Content

Status:

- Connected module inside Grabio.
- Supports restaurant discovery, brand authority, menus, events, private dining, and reservation conversion.
- Not a separate SEO platform.

Rules:

- SEO reads from restaurant/store content where possible.
- Content roles stay scoped.
- Public claims and metrics require source files in `reporting/data/`.

## Maintenance-Only Areas

These areas stay maintained for current customers and existing commitments, but they are not the growth roadmap.

- Shop / retail.
- Manufacturing / factory.
- Existing builder clients.
- Existing accounting and inventory clients.

Allowed work:

- Bug fixes.
- Security fixes.
- Stability fixes.
- Client-committed maintenance.
- Small compatibility changes needed to avoid breakage.

Avoid:

- New broad roadmap expansion.
- New marketing push.
- New generic vertical features unless they directly support the restaurant core.

## Dropped / Deferred Active Growth

These should not receive new active roadmap investment unless Anwar explicitly reopens them:

- NGO.
- Freelancer.
- Mini shop.
- Publisher/custom broad verticals.

Do not delete code only because a vertical is deferred. Hide, de-prioritize, or mark as maintenance/deferred through product maps and package gating.

## Restaurant Maturity Stages

### Stage 1 - Daily Operations

For a new fine-dining client starting without finance or inventory.

Includes:

- Reservations.
- Guest CRM.
- Staff and role access.
- Orders/service tracking.
- Daily reports and notes.
- Website/template/SEO if part of the service.

Excludes by default:

- Accounting.
- Inventory valuation.
- Full purchasing.
- GL/finance reports.

### Stage 2 - Operational Control

Adds:

- Recipes.
- Item/menu costing.
- Stock visibility.
- Supplier purchasing.
- Waste/spoilage/adjustment tracking.
- Staff cost and service-line reporting.

### Stage 3 - Finance Integration

Adds:

- Accounting mode.
- Vouchers and GL.
- Financial reports.
- Inventory valuation hooks.
- AR/AP where relevant.
- Owner/accounting-manager reporting.

### Stage 4 - Multi-Unit / Advanced Dining

Adds:

- Multi-branch.
- Multi-warehouse.
- Group CRM.
- Central kitchen or production support.
- Advanced role policy.
- Cross-location reporting.

### Stage 5 - Premium Intelligence

Adds:

- Advanced guest intelligence.
- Predictive follow-up.
- Event/private dining automation.
- Service-quality analytics.
- Executive dashboards.
- AI-assisted setup and operations.

## Security Structure Direction

Restaurant roles should be first-class platform roles, not one-account exceptions.

Target roles:

- Owner.
- General manager.
- Floor manager.
- Host / reservation.
- Waiter / service staff.
- Kitchen.
- Cashier.
- CRM / guest relations.
- Accounting.
- Inventory / purchasing.
- Builder / content / SEO.
- Support / implementation.

Every role must define:

- Store scope.
- Environment scope.
- Route access.
- Read/write actions.
- Sensitive field visibility.
- Mobile access.
- POS impact.
- Backend enforcement.

Environment scope matters:

- Production restaurant.
- Builder/demo workspace.
- CRM workspace.
- Accounting workspace.
- Mobile workspace.
- POS/device workspace.

## UI Structure Direction

The main admin should feel restaurant-first.

Primary navigation should move toward:

- Today / Daily Operations.
- Reservations.
- Guests / CRM.
- Service / Orders.
- Kitchen.
- Staff.
- Reports.
- Website / Content / SEO.
- Settings.

Optional module groups:

- Inventory.
- Purchasing.
- Accounting.
- Finance.
- Manufacturing/shop legacy modules where enabled for existing clients.

Finance and inventory should not dominate the first experience for restaurants that did not buy those modules.

## Feature Intake From Real Client Work

New fine-dining features should come from real operational drafts, Excel files, staff workflows, and client pain.

Before coding, classify each request as:

- Daily operation.
- CRM.
- Tenant option.
- Report.
- Automation.
- Role/security.
- Setup/import.
- Optional inventory.
- Optional accounting/finance.
- Temporary exception.

Every real data number or client-facing claim must have source evidence under `reporting/data/`.

## Engineering Rules

1. Restaurant/fine dining is the active product center.
2. CRM is core, not optional.
3. Accounting and inventory stay optional and can be activated later.
4. Builder/template/SEO stay connected modules for high-end clients.
5. Broad vertical expansion is paused.
6. Existing clients must not break because of the pivot.
7. Tenant settings, role policy, and resolver contracts still govern all changes.
8. Do not hardcode the new restaurant client into shared code.
9. Do not build new fine-dining features before reviewing the real client workflow draft.
10. Update this map when the restaurant workflow changes.
