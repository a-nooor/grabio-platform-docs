# 2026-07-25 — Nipco AP 201 payment-relief gap (deferred)

**Store:** Nipco `DfIhBAEZ5NR7yNX0HboZvv58Nf82`

**Problem:** Admin **Purchases** marked **paid** in ops, but GL **201** was never relieved (missing `purchase_payment` / equivalent GL). AP Aging (Option B) correctly shows **~$34,146.76** open on **5** platform purchases; GL **201** remains **~$195,899.53** — variance **~$161,752.77** is not a subledger bug.

**Scope (when scheduled):**
1. JE-level audit: every `purchase` receive vs payment vs 201/102/106 lines.
2. FG-style correcting entries for confirmed paid-not-relieved amounts (after full audit).
3. Re-proof AP Aging vs 201 post-correction.

**Priority / blocking:**
- **After** Cash Flow Statement ships and owner review.
- **Does not block** AP Aging Option B prod or Cash Flow staging.

**Proof reference (subledger, not fix):** `node scripts/verifyAgedPayablesE2E.cjs --store-id=DfIhBAEZ5NR7yNX0HboZvv58Nf82 --as-of=2026-07-25`

**Related:** AP Aging reads `purchases` collection (Option B) — 2026-07-25 staging.
