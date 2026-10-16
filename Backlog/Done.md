# Backlog — Done (recent)

Move items here when closed; prune entries older than ~30 days.

---

## 2026-09-10 — Internal Demo OS + marketing demo stores (prod)

- **SEO Phase 2:** sitemap index split, index policy, 10 priority prerender pages, programmatic quality gates (deployed earlier same day)
- **Public mock previews:** `/demo/:slug/app`, `/features/:moduleId/app` (15 URLs)
- **Marketing demo storefronts:** `scripts/seedMarketingDemoStores.cjs` → `grabio-demo-shop|cafe|restaurant|manufacturing|ecommerce`
- **Internal Demo OS Phase 1:** `/demo-os` + 12 modules; vertical tours `/demo/:slug/os/:moduleId`; sign-in gate; sitemap + prerender (+13 shells, 48 total)
- **Deployed:** `firebase deploy --only hosting` + `functions:api` on `market-flow-7b074`
- **Live:** https://grabio.space/demo-os , https://grabio.space/demo/shop/os/dashboard
- **Ref:** repo `README.md`, `decision-log.md`, `architecture.md`

## 2026-07-09 — Eco sys stripped from grabio.space PR

- Removed `the eco sys/` from PR #1 (0 paths in compare)
- Pushed ecosystem snapshot to `ecosystem.git` @ `baeb01b`
- Added `.gitignore` for ecosystem tree
- **Ref:** [[Decision-Log/2026-07-09-repo-boundary-split]]

## 2026-07-09 — PR #1 merged to main

- Owner approved `.env.production` diff (no secrets)
- PR #1 merged: https://github.com/AynBeirut/grabio.space/pull/1
- Merge commit on `main`: `bfb4fa48d9813fd4bdfd2dab9f41b44a4b66e700`
- Cleaned merge side effect: removed accidental `suba eco sys` gitlink before merge

## 2026-07-09 — Legacy audit account granted full platform access

- Email: `Maisabanna@gmail.com`
- Firebase UID: `FT5kK83C6sQcLvHgGr2GWLRIFeh1`
- Access: seller role `admin`, `business` + `active`, modular-v2 with all modules enabled
- Applied as user-level platform access only (no developer/repo permissions)

## 2026-07-13 — Restaurant 1-year subscription granted

- Email: `jinandaw86@gmail.com`
- Firebase UID: `ujff7blWYvUvlekQOrybvNCnn9V2`
- Account had `sellers/admin` doc but **no storeProfile** — profile created as part of grant
- Subscription: `pro` + `active`, workflow `live_kitchen` (`pkg_live_kitchen`), ends 2027-07-13
- Modules: invoicing, marketplace, analytics, payments, delivery, stock, restaurant, pos
- Real 1-year sub (not legacy) — will send renewal reminders and expire unless renewed
- **Gotcha noted:** production uses legacy entitlement path (`VITE_ECOSYSTEM_MODULAR` off) → `restaurant` module requires `pro` tier

## 2026-07-08 — POS installer + API live

- Storage: `pos/Grabio-POS-Setup.exe` (200 OK)
- Functions deployed with POS routes + storeCommerceGuard
- Admin `PosPairing.tsx` wired
- **Ref:** [[Decision-Log/2026-07-08-storeCommerceGuard-pos-api]]

## 2026-07-09 — Obsidian vault created

- `~/Documents/grabio-platform-docs/` — canonical docs
- **Ref:** [[Decision-Log/2026-07-09-obsidian-vault-canonical-docs]]
- Pushed private repo: https://github.com/AynBeirut/grabio-platform-docs
