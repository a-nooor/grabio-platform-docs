# 2026-07-08 — storeCommerceGuard + POS API on production path

**Context:** Commerce APIs needed subscription/demo guards; POS pairing and sync were stubbed or missing on live API.

**Decision:**
- Add `functions/src/services/storeCommerceGuard.ts` — pure eligibility check + Firestore loader
- Ship POS routes: `posSync`, `posCatalog`, `posOrders`, `posDeviceAuth`
- Admin pairing page: 6-digit code flow (`PosPairing.tsx`, `posApi.ts`)
- Upload POS installer to Firebase Storage `pos/Grabio-POS-Setup.exe`
- Deploy functions + rules before client POS testing

**Rejected alternatives:**
- Client-only guards — insufficient; server must enforce
- `pairing.json` as primary merchant UX — kept as advanced/first-install only; 6-digit code is normal path

**Consequences:**
- PR #1 bundles guard + modular work + builder (440 files) — owner review before merge
- POS local DB is machine-wide (`C:\AynBeirutPOS-Data\`) — not per Windows user

**Repos affected:** grabio.space (functions, admin UI); ecosystem.git (POS client source)

**Links:** PR #1, [[Architecture/Integration-Map#POS (Windows)]]
