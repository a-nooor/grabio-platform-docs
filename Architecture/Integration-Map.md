# Integration Map

**Last updated:** 2026-07-09

## Finance (Invoice Manager) embed

| Layer | Location | Mechanism |
|-------|----------|-----------|
| Source | `the eco sys/finance/beirut-finance-flow-main/` | ecosystem.git |
| Build | `npm run build:invoice` | Outputs to `dist/invoice/` |
| Dev alias | `vite.config.ts` + `src/vite-finance-alias.ts` | Resolves `@invoice-app` to finance `src/` |
| Bridge | `src/embed/FinanceAppBridge.tsx`, `financeFirebaseBridge.ts` | Shared Firebase session |
| Admin routes | `/admin/finance/*` | `FinanceModuleShell` inside `AdminLayout` |
| Standalone | `/invoice/*` | TWA / Play Store only |

## POS (Windows)

| Layer | Location | Mechanism |
|-------|----------|-----------|
| Client | `the eco sys/ecosystem-plan/posfinal-main/pos-v1/` | Electron + SQL.js offline |
| Pairing UI | `src/pages/admin/PosPairing.tsx` | 6-digit code (primary) |
| API | `functions/src/api/posSync.ts` etc. | Device token auth |
| Installer | Firebase Storage `pos/Grabio-POS-Setup.exe` | Download from admin |
| Contract | `docs/planning/pos-sync-contract.md` (grabio.space) | Canonical API shapes |

## storeCommerceGuard

| Consumer | Guard |
|----------|-------|
| Checkout APIs | `evaluateStoreCommerceEligibility()` |
| POS catalog/orders | Store must be non-demo, active subscription |
| Tests | `scripts/testStoreCommerceGuard.cjs` |

## Auth

- Google OAuth → Firebase Auth
- Store ID from `storeProfiles/{uid}`
- Module gates: `src/lib/entitlements.ts` + `functions/src/lib/entitlements.ts`

## Mobile

- `grabio-mobile/` — admin app; invoice via `GatedInvoiceManagerScreen`
- Shares entitlements pattern with web

## Supabase stack (parallel, not wired to prod)

- `suba eco sys/grabio-platform` — separate auth/data path
- No integration with `market-flow-7b074` in production
