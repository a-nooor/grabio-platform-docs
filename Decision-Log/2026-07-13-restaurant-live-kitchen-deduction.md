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

## Update — live data findings + additional fixes (same day)

Snapshot of the client store (`ujff7blWYvUvlekQOrybvNCnn9V2`, jinandaw86) revealed the code fix alone was **not sufficient**:
- Composed product `fajita` had **`recipeId = none`** — recipe existed (`tnlR4hHJRgt4EZQJwigE`, tomato 0.3 + bread 1, yield 1) but was never linked to the product. `composedProducts` collection empty. This is the "where do I attach the recipe?" gap.
- Raw materials had `currentStock = 0` (nothing to deduct).

Actions taken:
1. Data fix (`scripts/fixFajitaLinkAndStock.cjs`): set `products.recipeId`, and temp test stock bread=100, tomato=50 (client overwrites via import).
2. **UX fix** `src/pages/admin/AdminProducts.tsx`: added recipe `<Select>` to the **create** dialog (was only in edit). Falls back to a "create a recipe first" hint when none exist. Needs **hosting deploy**.
3. **Trigger gap** `functions/src/triggers/orderNotifications.ts`: `onOrderCreated` did not run deduction, so orders created already-`paid` (admin/POS one-step) never deducted. Added deduction on create (idempotency key prevents doubles). **Deployed.**

Deploys done: `api`, `onOrderCreated`, `onOrderStatusChanged`. Pending: hosting deploy for the AdminProducts create-dialog recipe selector.

Read-only proof tool: `scripts/kitchenStockSnapshot.cjs --email <email>` (before/after a sale).

## Update 2 — stock model clarification + inline quick-add material

Owner clarified the product model (applies to **both** resto and manufacturing):
- Creating a **recipe** or a **product** does NOT require stock. Stock only matters at sale (resto) / production (factory). Recipe creation still requires ingredient **cost > 0** (for costing) — that's cost, not stock.
- Quick-add should be inline so users never leave the page.

Implemented in `src/pages/admin/AdminRecipes.tsx`:
- Ingredient material dropdown (both create + edit recipe dialogs) now has a **"+ Add new raw material"** option → opens a small inline dialog (name, unit, cost) → creates the `rawMaterials` doc with `currentStock: 0` (no stock forced), auto SKU/barcode, then auto-selects it into the ingredient row and syncs the unit.

Frontend build passes (`npm run build`). Both frontend changes (AdminProducts create-dialog recipe selector + AdminRecipes quick-add) ship together in the next **hosting deploy**.

## Update 3 — quick-add extended + hosting deployed

- Added the same inline "+ Add new raw material" quick-add to `src/pages/admin/AdminComposedProducts.tsx` (material row dropdown + empty-state button; removed the "Add Material disabled when no materials" dead-end).
- **Hosting DEPLOYED** (`firebase deploy --only hosting`, market-flow-7b074, https://market-flow-7b074.web.app). Ships: AdminProducts create-dialog recipe selector, AdminRecipes quick-add, AdminComposedProducts quick-add.
- Note: PWA — client may need a hard refresh to pick up the new bundle.

Runtime-proof for the deduction still pending one real test sale of fajita (owner to perform).

**Repos affected:** grabio.space (functions + frontend)
