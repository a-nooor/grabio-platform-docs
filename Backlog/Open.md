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
| **Item** | Full bank rec: statement import/entry, match to GL **106/105** (optional **102** later), unmatched bank/book items, reconciliation report |
| **Effort** | **12–18 dev-days** MVP (+ **4–6** if **102** or multi-account in v1) |
| **Dependency** | **Cash on Hand** ops snapshot vs GL **102** gap ([[Decision-Log/2026-07-25-reconciliation-cash-ar-gaps]]) — affects whether POS cash belongs in bank rec scope |
| **Priority** | **Not now** — future capability; **Cash Collection** deposit tracking already works (E-Service proof 2026-07-25) |
| **Note** | Distinct from Accounting → Reconciliation (GL vs AR/AP aging snapshots) and from today’s gap-closing ship list |

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
