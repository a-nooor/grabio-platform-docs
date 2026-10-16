# 2026-09-15 - Fine-Dining Restaurant Pivot

## Context

Anwar signed a new 3-star restaurant client for daily operations management.

The client will start without Grabio accounting, inventory, or financial functions. Those modules already exist and work for current needs, but they should not define the first experience for this restaurant.

The product direction changes from broad ERP/marketplace expansion toward fine-dining restaurant operations plus CRM.

## Decision

Grabio's active product center becomes:

- Fine-dining restaurant daily operations.
- Guest CRM and relationship intelligence.
- Reservation, service, order, staff, daily report, and follow-up workflows.
- Optional accounting, finance, inventory, purchasing, recipes, costing, payroll, and multi-branch maturity modules.
- Connected builder/template/SEO/content modules for high-end clients.

Grabio will not actively push or expand NGO, freelancer, mini shop, publisher, or broad custom verticals unless Anwar explicitly reopens them.

Shop, manufacturing, builder, accounting, and inventory remain maintained for actual customers and existing commitments.

## Builder / Template / SEO Decision

Do not split builder, template, and SEO into a separate platform now.

Keep them connected inside Grabio as gated high-end client modules because they share:

- Tenant identity.
- Store profile.
- Domain and brand settings.
- Menu/products/content.
- Reservations.
- CRM and guest follow-up.
- Role and environment policy.

Splitting can be reconsidered only if builder/SEO becomes a standalone business with separate customers, billing, team, roadmap, and data boundaries.

## Consequences

- New UI structure should feel restaurant-first, not generic ERP-first.
- New security structure should define restaurant-native roles and environment scopes.
- Finance and inventory must be optional/off for restaurants that did not activate them.
- Future fine-dining features should come from real client workflow drafts, Excel files, and operational pain.
- Existing modules should be hidden, gated, maintained, or de-prioritized, not deleted.
- Future agents must update `Fine-Dining-Platform-Map.md` when restaurant workflow, CRM, setup, role, or module behavior changes.

## References

- `~/Documents/grabio-platform-docs/Architecture/Fine-Dining-Platform-Map.md`
- `~/Documents/grabio-platform-docs/Architecture/Packages-Workflows-Modules.md`
- `/home/anwar/Documents/grabio space/decision-log.md`
