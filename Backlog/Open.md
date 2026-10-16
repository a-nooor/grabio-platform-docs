# Backlog — Open

**Last synced:** 2026-09-15 (fine-dining restaurant pivot)

---

## grabio.space `#grabio`

### P0 - Fine-dining restaurant pivot map

| Field | Value |
|-------|-------|
| **Item** | Re-center Grabio roadmap, UI, security, and setup around fine-dining restaurant daily operations plus CRM |
| **Context** | New signed 3-star restaurant starts with daily operations management, not accounting/inventory/finance. Accounting and inventory remain optional later modules. Broad vertical growth is paused. |
| **Done when** | Product/docs map is updated; active/deferred/maintenance modules are classified; restaurant roles and UI navigation are planned; builder/template/SEO stay connected as gated high-end client modules |
| **Ref** | [[Architecture/Fine-Dining-Platform-Map]], [[Architecture/Packages-Workflows-Modules]], repo `decision-log.md` 2026-09-15 product pivot |

### P0 - Restaurant security and role model

| Field | Value |
|-------|-------|
| **Item** | Define restaurant-native roles and permissions before new fine-dining UI/features |
| **Context** | Fine-dining operations need owner, general manager, floor manager, host/reservation, waiter, kitchen, cashier, CRM/guest relations, accounting, inventory/purchasing, builder/content/SEO, and support roles |
| **Done when** | Roles define store scope, environment scope, route access, read/write actions, sensitive-field visibility, mobile access, POS impact, and backend enforcement |
| **Ref** | [[Architecture/Fine-Dining-Platform-Map]], [[Architecture/Role-Permission-Environment-Policy]], [[Architecture/Resolver-Contracts]] |

### P0 - Restaurant-first admin UI map

| Field | Value |
|-------|-------|
| **Item** | Redesign admin information architecture around daily operations and CRM, with finance/inventory optional |
| **Context** | A restaurant that did not activate accounting or inventory should not feel forced into generic ERP screens |
| **Done when** | Navigation/setup plan exists for Today/Daily Operations, Reservations, Guests/CRM, Service/Orders, Kitchen, Staff, Reports, Website/Content/SEO, Settings, and optional Finance/Inventory |
| **Ref** | [[Architecture/Fine-Dining-Platform-Map]] |

### P0 — Mobile Play: manager sub-account back-office parity

| Field | Value |
|-------|-------|
| **Item** | Ship Grabio admin app (`space.grabio.app`) with manager = store admin on mobile (same as web) |
| **Context** | Play **1.3.5** `ownerAccess.ts` is owner-only; managers (`sub_manager`) blocked from Purchases/Expenses/Accounting gates. Firestore LH manager binding is correct. |
| **Done when** | Play release versionCode **≥ 140** live; Little Hands manager verifies from **Play only** (no sideload); evidence JSON updated |
| **Ref** | Repo `reporting/data/platform-pos-discovered-fixes-2026-09-14.md`, `littlehands-manager-mobile-permission-root-cause-2026-09-13.json` |

### P1 — Windows POS vs cloud manager roles

| Field | Value |
|-------|-------|
| **Item** | Document or implement link between Firebase `subAccounts` (manager) and POS local roles |
| **Context** | `posfinal-main/pos-v1` uses SQL cashier/manager/admin — separate from `manager@grabio.space` |
| **Done when** | Product decision recorded; if needed, pairing or staff sync spec in `docs/planning/pos-sync-contract.md` |
| **Ref** | Repo `reporting/data/platform-pos-discovered-fixes-2026-09-14.md` § POS |

### P1 — Platform tenant/role cleanup after manager mobile fix

| Field | Value |
|-------|-------|
| **Item** | Convert manager/tenant discoveries into platform-safe web and account rules |
| **Context** | Duplicate `manager@` sub-account email exists across Little Hands and NIPCO; some web admin routes still use `user.role === 'admin'`; subscription/billing should remain owner-only by design |
| **Done when** | Duplicate manager email risk is removed or aliased; tenant binding uses `users.subAccountId` before email fallback; admin route checks use store-admin helpers where intended; subscription owner-only behavior is documented in UI/docs |
| **Ref** | Repo `reporting/data/platform-pos-discovered-fixes-2026-09-14.md`, [[Backlog/Structural-PR-Slices]], [[Architecture/Role-Permission-Environment-Policy]] |

### P1 — Mobile store-admin parity leftovers

| Field | Value |
|-------|-------|
| **Item** | Audit mobile owner-only leftovers after Play manager parity release |
| **Context** | Manager parity needs follow-up beyond `ownerAccess`: CRM map, sales order policy, create order branches, and profile sub-account load order |
| **Done when** | Approved mobile back-office surfaces treat manager as store admin; mobile tenant resolution prefers `subAccountId` before email lookup; no Play/mobile route binds manager to the wrong tenant |
| **Ref** | Repo `reporting/data/platform-pos-discovered-fixes-2026-09-14.md`, [[Backlog/Structural-PR-Slices]] |

---

### Demo OS — Phase 2 (16 additional admin screens)

| Field | Value |
|-------|-------|
| **Item** | Expand public read-only admin demo beyond first 12 modules |
| **Context** | Phase 1 live: `/demo-os` + 12 modules (dashboard → AI). Buyers still cannot preview analytics, revenue, reports, customers, payments, suppliers, returns, restaurant/manufacturing flows, content creator, SEO audit, etc. |
| **Done when** | Next 16 screens added to `demoOsCatalog.ts` with SEO copy, sitemap/prerender entries, vertical filters, and sign-in gate; browser-verified on prod after deploy |
| **Ref** | Repo `decision-log.md` → Internal Demo OS; `src/data/marketing/demoOsCatalog.ts` |

### SEO — GSC re-check after demo-os deploy

| Field | Value |
|-------|-------|
| **Item** | Export GSC Pages + Sitemap after `/demo-os/*` crawl |
| **Context** | Phase 2 sitemap now includes 13 demo-os URLs (48+ static shells). Prior baseline: 16 indexed (`reporting/data/grabio-gsc-indexing-baseline-2026-09-10.json`) |
| **Done when** | New evidence JSON in `reporting/data/` with discovered count and indexed demo-os URLs |
| **Ref** | [[Architecture/SEO-Sitemap-Index-Policy]] |

### Workspace health - inventory and quarantine

| Field | Value |
|-------|-------|
| **Item** | Inventory workspace clutter and propose safe organization without data loss |
| **Context** | Workspace contains main code, mobile apps, invoice app, vendor copies, sub backup/main structure, client data, reporting evidence, backups, and loose docs |
| **Done when** | Inventory report exists; protected roots are listed; proposed move list is approved; quarantine batches include manifest with original path, reason, move date, review date, delete approval status, and restore notes |
| **Rule** | 40-day quarantine means review eligibility only; no automatic deletion without explicit Anwar approval |
| **Ref** | [[Architecture/Developer-Landing-Map]], [[Architecture/Workspace-Organization-Policy]], [[Architecture/Workspace-Inventory-2026-09-10]], [[Decision-Log/2026-09-10-workspace-organization-quarantine-policy]] |

### Setup surfaces - profile, invoice, website separation

| Field | Value |
|-------|-------|
| **Item** | Review and clean separation between Store Profile setup, Invoice Document setup, and Website Template setup |
| **Context** | Setup was originally one Store Profile page, then split for performance and clarity. Invoice numbering still appears in Store Profile, invoice document setup owns A4/PDF branding, and website template setup spans Theme Editor plus legacy template page. |
| **Done when** | Each field has one owner, fallback rules are documented, invoice numbering ownership is decided, `AdminTemplates.tsx` vs `ThemeEditor.tsx` authority is clear, and no save path overwrites another surface's owned fields |
| **Ref** | [[Architecture/Setup-Surface-Separation]] |

### Roles and environments - general policy

| Field | Value |
|-------|-------|
| **Item** | Turn builder/accounting accounts, role permissions, and environment access into reusable platform rules |
| **Context** | Current builder/accounting role setup is about 60% complete: roles and route guards exist, but they are fixed code rules and can become one-account setup if not generalized |
| **Done when** | `ROLE_PERMISSIONS` becomes default role templates or a tenant role-policy model; builder/accounting environments are governed by shared policy; web, Functions, mobile, POS, and invoice app enforce the same effective permissions; admin UI exposes customization where package allows it |
| **Ref** | [[Architecture/Role-Permission-Environment-Policy]] |

### No-risk correction follow-up

| Field | Value |
|-------|-------|
| **Item** | Execute future structure corrections as small safe PR slices after the critical client accounting setup |
| **Context** | Today is docs/plans only. Tomorrow's old-client accounting setup must not be endangered by broad refactors, migrations, deploys, file moves, or production behavior changes. |
| **Done when** | Developer landing map exists; inventory-only map exists; resolver contracts are drafted; structural PR slices are documented; tomorrow's no-risk setup runbook exists |
| **Ref** | [[Backlog/Structural-PR-Slices]], [[Architecture/Resolver-Contracts]], [[Runbooks/Client-Accounting-Setup-No-Risk]] |

### Platform health — tenant options governance

| Field | Value |
|-------|-------|
| **Item** | Audit recent client-specific changes and move reusable behavior into typed tenant settings |
| **Context** | Jinan's Kitchen reservations/advance orders, NIPCO order-status preferences, payment-method consistency, and mobile sub-account roles show platform options are needed |
| **Done when** | Each change is classified as global platform fix, tenant option, account data setup, or temporary exception; tenant options have defaults, admin controls, shared readers, and web/POS/mobile/Functions verification; repeated setup scripts have UI paths for template download, upload, validation preview, approval, and post-setup editing; ERP maturity gaps are tracked for module lifecycle, unified data core, multi-company/warehouse, stock valuation, and automation hooks |
| **Ref** | [[Decision-Log/2026-09-10-client-requests-tenant-options]], [[Architecture/Packages-Workflows-Modules]] |

### Invoice embed — Workstream B (staging QA)

| Field | Value |
|-------|-------|
| **Item** | Invoice Manager embed QA + B4 polish |
| **Blocker** | Owner file-list approval for hosting deploy (locked 2026-06-23) |
| **Open checks** | `npm run build` → `dist/invoice/`; `/admin/finance/invoices` embedded; session skip Hero; profile mapping; `templateColors` accents |
| **Ref** | [[Decision-Log/2026-06-23-invoice-embed-in-admin]] |

### PWA / admin cache

| Field | Value |
|-------|-------|
| **Item** | Verify no stale service-worker bundles after deploy |
| **Context** | AdminProducts permission errors traced to old cached JS |
| **Done when** | Post-deploy smoke on `/admin/products` with hard refresh / SW bump |

### Nipco — paid purchases not relieved from GL 201

| Field | Value |
|-------|-------|
| **Item** | JE audit + correcting entries for ops-paid purchases still on **201** (~**$161k** GL vs ~**$34k** open AP subledger) |
| **Blocker** | None — schedule when Nipco 201 audit is prioritized |
| **Ref** | [[Decision-Log/2026-07-25-nipco-ap-201-payment-relief-gap]] |
| **Proof (subledger)** | `verifyAgedPayablesE2E.cjs` on Nipco store id `DfIhBAEZ5NR7yNX0HboZvv58Nf82` |

### Reconciliation — Cash on Hand & AR subledger vs GL

| Field | Value |
|-------|-------|
| **Item** | Align **102** ops cash snapshot + **110** AR subledger with GL (or document intentional cash-first policy) |
| **Blocker** | None — **out of scope for AP Aging + Cash Flow prod release (2026-07-25)** |
| **Ref** | [[Decision-Log/2026-07-25-reconciliation-cash-ar-gaps]] |
| **Example (Nipco)** | Cash GL **$47,594.50** vs ops **$0**; AR subledger **$33.60** vs GL **$0** |

### Depreciation MVP (fixed-asset register)

| Field | Value |
|-------|-------|
| **Status** | **Shipped prod 2026-07-25** — Accounting → Depreciation tab |
| **Proof** | `verifyDepreciationE2E.cjs` (Dr **710** / Cr **156**, idempotent); pilot data cleaned on E-Service |

### GL / vouchers — shipped 2026-07-25

| Field | Value |
|-------|-------|
| **Gapless voucher serials** | **Done** — voucher number allocated inside successful `postJournalEntry` Firestore transaction only |
| **JE `event` field** | **Done** on new posts — stored on `journalEntries.event`; legacy rows may still be blank (`sourceKey` retains event segment) |

### Real bank reconciliation (statement import + matching)

| Field | Value |
|-------|-------|
| **Status** | **Phase 1 in progress** (staging → E-Service proof) |
| **Plan** | [[Decision-Log/2026-07-25-bank-reconciliation-phased-plan]] |
| **Item** | Full bank rec: statement import/entry, match to GL **106/105** (optional **102** later), unmatched bank/book items, reconciliation report |
| **Effort** | **12–18 dev-days** MVP (+ **4–6** if **102** or multi-account in v1); Phase 1 alone **5–7** |
| **Dependency** | **Cash on Hand** ops snapshot vs GL **102** gap ([[Decision-Log/2026-07-25-reconciliation-cash-ar-gaps]]) — Phase 4 |
| **Note** | Distinct from Accounting → Reconciliation (GL vs AR/AP aging snapshots) and from Cash Collection deposits |

---

## ecosystem.git `#ecosystem`

### Finance checkout for CI / new devs

| Field | Value |
|-------|-------|
| **Item** | Document + optionally script sibling clone of ecosystem for `build:invoice` |
| **Blocker** | None — docs in [[Gotchas/Fresh-Clone]]; optional `scripts/ensure-ecosystem-checkout.sh` |
| **Done when** | Fresh clone build passes with documented steps |

### POS Windows client — Grabio sync path

| Field | Value |
|-------|-------|
| **Item** | POS `grabio-pairing.js` / `grabio-sync.js` in `pos-v1` |
| **Open** | 6-digit pairing QA on paired store; catalog pull; order push |
| **Ref** | `ecosystem-plan/pos-windows-builder-pack/` on ecosystem.git |

---

## suba eco sys `#suba`

### R2 image uploads

| Field | Value |
|-------|-------|
| **Item** | Cloudflare R2 keys in Supabase Edge Function secrets |
| **Blocker** | Credentials not in repo — owner provides keys |
| **Done when** | Image upload works on grabio.online test stack |

### Production cutover

| Field | Value |
|-------|-------|
| **Item** | 1-week test pass before any prod consideration |
| **Blocker** | R2 + full regression on Supabase stack |
| **Rule** | Never touch `the eco sys/` for Supabase experiments |

---

## Not in Open (deferred / aspirational)

These stay **out** until explicitly scheduled:

- Sales CRM add-on, dropship import, full modular manifest split, SEO phase 1 checklist items, BOM/production workflow — see legacy `backlog.md` archive
