# 2026-07-25 — Bank reconciliation phased plan (approved)

**Status:** Phase 1 in progress (staging first).

**Context:** [[Decision-Log/2026-07-25-bank-reconciliation-future-scope]] — distinct from Cash Collection (`/admin/cash-collection`) and Accounting → Reconciliation (GL vs AR/AP aging).

## Phases

| Phase | Scope | Estimate | Exit proof |
|-------|--------|----------|------------|
| **1** | Period + account (**106/105**); statement manual + CSV; book lines from posted JEs; summary totals; Firestore sessions | **5–7 dev-days** | Staging + E-Service (`Av22LKyet8QmVcu9b8Njz1HVfoy1`); `verifyBankRecPhase1E2E.cjs` |
| **2** | Matching engine (1:1, date/amount window, manual link) | **4–6** | Matched pairs persisted; unmatched lists |
| **3** | Rec report, lock session, opening/closing variance | **3–4** | Locked session immutable |
| **4** | **102**, multi-account polish, export | **4–6** | Policy on POS cash vs GL |
| **Total MVP** | | **~12–18** | Prod after owner sign-off per phase |

## Phase 1 — in / out

**In:** Accounting tab **Bank Rec**; `bankRecSessions` + `statementLines` subcollection; CSV columns `date, amount, description, ref` (+ optional `dr`/`cr` or signed amount).

**Out:** Matching, mark reconciled, **102**, bank feeds, edit posted JEs.

## Proof store

- **E-Service:** `Av22LKyet8QmVcu9b8Njz1HVfoy1` (slug `ayn-beirut`).

## Dependencies

- **102 ops vs GL** — deferred to Phase 4 ([[Decision-Log/2026-07-25-reconciliation-cash-ar-gaps]]).

## Phase 1 proof (2026-07-25)

- **Staging:** https://market-flow-7b074--staging-76tya5kx.web.app → `/admin/finance/accounting` → **Bank Rec** tab.
- **Script:** `node scripts/verifyBankRecPhase1E2E.cjs` on store `Av22LKyet8QmVcu9b8Njz1HVfoy1`.
- **Book (106, Jul 2026):** 4 posted lines (incl. **Dr 100** cash collection 2026-07-25); net **181**.
- **Statement session:** `BR-106-2026-07-01-2026-07-31` + 2 manual lines (net **99**); difference informational only in Phase 1.
- **Firestore rules:** `bankRecSessions` + `statementLines` deployed.
- **Prod:** not deployed — owner sign-off after staging UI smoke.

## Phase 1 prod (2026-07-25)

- **Prod hosting** deployed (`grabio.space` → Accounting → **Bank Rec**).
- E-Service proof session **cleaned** (`verifyBankRecPhase1E2E.cjs --cleanup`).

## Phase 2 prod (2026-07-25)

- **Prod hosting** includes Phase 1 + Phase 2 (matching).

## Phase 3 (staging)

- Reconciliation **report** (book opening/closing, matched/outstanding, closing variance).
- **Statement opening balance** on session; **Lock reconciliation** (immutable stmt/matches).
- Proof: `verifyBankRecPhase3E2E.cjs` (after UI session exists).
