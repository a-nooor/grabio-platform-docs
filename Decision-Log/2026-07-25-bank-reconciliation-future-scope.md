# 2026-07-25 — Real bank reconciliation (future scope)

**Context:** Admin **Cash Collection** (`/admin/cash-collection`) records order cash → bank deposit and posts **Dr 106 / Cr 102**. E-Service proof 2026-07-25 confirmed deposit tracking + GL (`cash_collection:deposited`). This is **not** statement-based bank reconciliation.

**Future MVP (not scheduled):**
- Import or enter **bank statement lines** (CSV + manual); reconcile GL cash accounts (**106/105** primary).
- Auto + manual **matching** to posted journal lines; **unmatched** bank (fees, timing) and book items.
- Reconciliation **report** (opening, cleared, outstanding, statement closing variance); optional “marked reconciled” session.

**Estimate:** **12–18 dev-days** (+ **4–6** if **102** or multi-account in v1).

**Dependency:** Resolve or define policy for **Cash on Hand** ops vs GL **102** before including POS drawer in scope — [[Decision-Log/2026-07-25-reconciliation-cash-ar-gaps]].

**Priority:** Backlog only — owner to schedule after higher-priority work.
