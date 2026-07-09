# Backlog — Open

**Last synced:** 2026-07-09 (post PR #1 merge)

---

## grabio.space `#grabio`

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
