# 2026-07-25 — Reconciliation subledger gaps (deferred)

**Context:** After AP Aging Option B + Reconciliation aligned AP to aging totals, Nipco prod smoke (2026-07-25) still shows variances on **Cash on Hand** and **AR** — out of scope for AP/Cash Flow release.

**Known gaps (do not fix in AP/CF tranche):**

| Row | GL | Subledger source | Typical symptom |
|-----|-----|------------------|-----------------|
| Cash on Hand | **102** (etc.) | `AccountingContext` / ops cash snapshot | GL has balance; ops subledger **$0** if POS/collections not wired to reconciliation |
| Accounts Receivable | **110** | AR Aging (`financeInvoices` + platform orders) | Small open invoice balance (e.g. **$33.60**) vs **$0** GL when sales post cash-first without 110 |

**Nipco AP 201** (~**$161k** variance) is a separate data/GL relief issue — [[Decision-Log/2026-07-25-nipco-ap-201-payment-relief-gap]].

**When to schedule:** After depreciation posting scoping/approval, or dedicated reconciliation hardening sprint.
