# grabio.space

**Remote:** `https://github.com/AynBeirut/grabio.space.git`  
**Local:** `~/Documents/grabio space/`  
**Firebase project:** `market-flow-7b074`

## What lives here

| Area | Paths | Notes |
|------|-------|-------|
| Main web app | `src/` | React + Vite admin, storefront, builder |
| Cloud Functions | `functions/src/` | API, webhooks, `storeCommerceGuard`, POS sync |
| Security rules | `firestore.rules`, `storage.rules` | Deploy with functions/hosting |
| Mobile admin | `grabio-mobile/` | Expo / React Native |
| White-label | `white-label-client-app/` | Client app variant |
| Integration stubs | `src/embed/`, `src/vite-finance-alias.ts` | **Imports** finance from disk, not from git |
| Planning stubs | `docs/planning/` | Pointers; canonical docs in this vault |

## What does NOT live here (git)

- `the eco sys/` — entire tree gitignored → [[Architecture/ecosystem.git]]
- `suba eco sys/` — separate nested repo
- `.env`, `.credentials.md`, release APK/AAB binaries

## Active branch / PR

- **Branch:** `feat/ecosystem-modular-local`
- **PR #1:** [storeCommerceGuard + modular](https://github.com/AynBeirut/grabio.space/pull/1) — **OPEN, not merged**
- Post-cleanup: 440 files, **0** `the eco sys/` paths

## Key production modules (in-repo)

- `storeCommerceGuard` — subscription/demo eligibility on commerce APIs
- POS API — `posSync.ts`, `posCatalog.ts`, `posOrders.ts`, `posDeviceAuth.ts`
- Admin POS pairing — `src/pages/admin/PosPairing.tsx`, `src/lib/posApi.ts`
- Modular entitlements — `src/lib/entitlements.ts`, `functions/src/lib/entitlements.ts`

## Build

```bash
npm install
npm run dev          # :8080
npm run build        # requires finance checkout — see [[Gotchas/Build-Dependencies]]
firebase deploy      # only after [[Deploy/Protocol]] approval
```
