---
title: Setup surfaces must stay separated
date: 2026-09-10
repos: grabio.space, grabio-platform-docs
---

# 2026-09-10 - Setup surfaces must stay separated

**Context:** Store Profile setup originally held most setup fields. It was split for performance and clarity into Store Profile, Invoice Document setup, and Website Template setup. Review showed the split exists but is not fully clean: invoice numbering remains in Store Profile; invoice document branding is separate; website template setup spans Theme Editor and legacy template setup.

**Decision:** Treat the three setup surfaces as separate ownership areas. Store Profile owns business identity and operational defaults. Invoice Document setup owns A4/PDF document branding and template style. Website Template setup owns storefront theme and public layout. Shared fields may be used as fallbacks only when the authoritative edit surface is clear.

**Rejected alternatives:**

- Returning all setup fields to Store Profile - recreates the old heavy page and hurts performance/clarity.
- Letting multiple setup pages write the same field silently - creates overwrites and client-specific template bugs.
- Moving fields before ownership is documented - risks breaking invoice, website, mobile, POS, or NIPCO template lock behavior.

**Consequences:** Before coding, review field ownership, fallback order, read/write paths, mobile/POS consumers, scripts/backfills, and NIPCO lock impact. Invoice numbering needs an explicit decision: move to Finance/Invoice settings or document it as operational order numbering separate from A4/PDF template setup.

**Repos affected:** grabio.space | grabio-platform-docs

**Links:** [[Architecture/Setup-Surface-Separation]], [[Backlog/Open]]
