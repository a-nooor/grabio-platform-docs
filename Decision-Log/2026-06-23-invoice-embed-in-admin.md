# 2026-06-23 — Invoice Manager embed in admin (not linked app)

**Context:** Invoice Manager was a separate SPA at `/invoice/`; poor UX vs unified admin.

**Decision:**
- **Primary web UX:** `/admin/finance/*` inside `AdminLayout` + `FinanceModuleShell`
- **Standalone `/invoice/`:** TWA / Play Store build only
- **Profile:** Single source `storeProfiles/{storeId}` — no `localStorage` company authority
- **Build:** `build:invoice` chained in root `npm run build` → `dist/invoice/`
- **Deploy gate:** No hosting deploy until owner approves file list (Workstream B)

**Rejected alternatives:**
- Linked app / new tab as primary — rejected
- Duplicate company profile in IM — rejected; Admin Profile only

**Consequences:**
- Vite must resolve finance source from disk ([[Gotchas/Build-Dependencies]])
- Phases B1–B5 in legacy backlog; track open items in [[Backlog/Open#grabio.space]]

**Repos affected:** grabio.space (embed wiring), ecosystem.git (finance source)
