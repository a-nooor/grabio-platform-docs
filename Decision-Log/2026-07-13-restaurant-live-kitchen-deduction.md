# 2026-07-13 — Restaurant (live kitchen) sells without production

**Context:** A restaurant client (`jinandaw86@gmail.com`) was set up but composed dishes behaved like a factory — stock only moved via a Production run. Owner: restaurants must deduct raw materials **at the moment of sale**, no production step. Sales run on **Grabio POS**.

**Root cause:** `functions/src/services/kitchenSaleDeduction.ts` (`deductComposedIngredientsOnSale`) existed and was wired (POS `posOrders`/`posSync` + storefront/admin paid trigger `orderNotifications`) but read the **wrong fields**, so it silently deducted nothing:
- read `recipe.ingredients` with `{ materialId }` — recipes actually store `ingredients` (Recipes page) or `materials` (auto from Composed Products), both keyed by `rawMaterialId`
- read/wrote raw material `.quantity` — real field is `.currentStock`
- ignored recipe yield (`outputQuantity`/`yieldQuantity`)

**Decision / fix:** Rewrote the deduction to:
- support both `ingredients` and `materials` shapes; accept `rawMaterialId` (fallback `materialId`)
- deduct from `currentStock` (fallback `quantity`)
- divide by recipe yield → correct per-sold-unit amount
- idempotent per `orderId_productId` (deterministic doc in `stores/{id}/kitchenDeductions`) so re-fired triggers never double-deduct

**Gates (unchanged, confirmed correct for this client):**
- requires `storeProfiles.businessWorkflow === 'live_kitchen'`
- skips if `composedProductSource === 'pos'` (POS handles its own stock)
- POS path only calls it when device `composedProductSource === 'platform'` (default)
- Does **not** depend on `VITE_ECOSYSTEM_MODULAR` (server reads profile directly)

**Rejected alternatives:**
- Forcing production/finished-goods for restaurants — wrong model for live kitchen
- Gating on modular flag — server path already independent of it

**Consequences / follow-ups:**
- **Needs `firebase deploy --only functions`** to take effect (pending owner approval).
- Runtime proof after deploy: make one POS sale of a composed dish → confirm a `rawMaterials.currentStock` dropped by recipe qty.
- Open follow-up: sell-side stock gating — ensure storefront/POS lets a `live_kitchen` composed product be sold based on available raw materials (not requiring produced finished-goods stock).
- New restaurants must be created with `businessWorkflow = 'live_kitchen'`.

**Repos affected:** grabio.space (functions)
