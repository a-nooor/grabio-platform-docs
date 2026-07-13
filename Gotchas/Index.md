# Gotchas — Index

Quick lookup. Detail in linked notes.

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `npm run build` fails — finance path missing | `the eco sys/` not on disk | [[Gotchas/Fresh-Clone]] |
| Vite can't resolve `@invoice-app` | Finance source missing | Clone ecosystem.git |
| Admin permission-denied on products | Auth token not ready OR stale SW bundle | `waitForAuthToken`; hard refresh / deploy new hosting |
| Toasts don't show in admin | Only Sonner mounted, shadcn `useToast` used | Mount Shadcn `Toaster` in `App.tsx` |
| POS pairs but sync empty | Skipped sync or wrong store; local SQL DB has old data | Use 6-digit code; Skip "Sync All Data" if testing clean |
| POS data visible across Windows users | DB path machine-wide `C:\AynBeirutPOS-Data\` | Expected; not per-user isolation |
| `git push` rejected after filter-repo | History rewrite | `git push --force-with-lease` (coordinate with team) |
| PR contains eco sys files | Boundary violation | [[Architecture/Repo-Boundaries]] |
| Admin profile save fails: `financeDocumentSettings.primaryColor` undefined | New store has no theme colors; save wrote `undefined` to Firestore | Defaults now patched on profile; code fix in AdminProfile + finance storeService (deploy hosting to ship) |
| Restaurant sale doesn't reduce raw material stock | `kitchenSaleDeduction` read wrong fields (`ingredients.materialId`, rawMaterial `.quantity`); requires `businessWorkflow='live_kitchen'` | Fixed to read `ingredients`/`materials` + `rawMaterialId` + `currentStock` + yield; needs functions deploy. See [[Decision-Log/2026-07-13-restaurant-live-kitchen-deduction]] |

## Stale PWA bundle

After hosting deploy, verify Network tab shows **new** chunk filenames. Old caches served `AdminProducts-B7fWS7aA.js`-style hashes and caused false "permission" errors.

## Build chain

See [[Gotchas/Build-Dependencies]].

## New machine

See [[Gotchas/Fresh-Clone]].
