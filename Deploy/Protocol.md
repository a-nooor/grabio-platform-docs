# Deploy Protocol

**Last updated:** 2026-07-09  
**Authority:** Non-negotiable unless owner explicitly overrides in writing.

## Gates (all must pass)

### 1. Explicit approval

- **No** `git push` to `main` without owner confirmation that tests passed
- **No** `firebase deploy` (hosting, functions, rules, storage) without explicit owner OK
- **No** merge PR without boundary check ([[Architecture/Repo-Boundaries]]) and review

### 2. Runtime proof required

"Logic appears correct" or "reviewed in IDE" is **not** sufficient for production.

Valid proof examples:

| Change type | Minimum proof |
|-------------|----------------|
| Firestore rules | `npm run test:firestore-rules` (emulator) OR live token test against rules |
| storeCommerceGuard | `node scripts/testStoreCommerceGuard.cjs` |
| API routes | `curl` / health check against deployed or emulated endpoint with expected status |
| Admin UI | Browser load of affected route after build; check network tab for 403 vs 200 |
| Hosting | Verify asset hash changed; hard refresh / SW cache per [[Gotchas/Index#Stale PWA bundle]] |

Invalid proof:

- "Deployed successfully" without hitting the changed behavior
- Assuming emulator = prod without rules deploy

### 3. Secrets

- Credentials **only** in local `.credentials.md` (gitignored)
- Never commit `.env`, `.env.production`, keystores, service accounts

### 4. Repo boundary pre-merge

```bash
git diff origin/main...HEAD --name-only | grep -E "the eco sys|LINUX-BUILDER|^pos-client"
# Must return empty for grabio.space PRs
```

### 5. Rollback awareness

- Know rollback path before deploy ([[Deploy/Checklists/hosting]], functions)
- Flag data migrations that are not reversible

## Deploy order (typical Firebase)

1. `firestore.rules` + indexes (if changed)
2. `functions` (API)
3. `hosting` (after `npm run build` succeeds locally)
4. `storage.rules` (if changed)

## Checklists

- [[Deploy/Checklists/hosting]]
- [[Deploy/Checklists/functions]]
- [[Deploy/Checklists/firestore-rules]]

## Runtime proof detail

See [[Deploy/Runtime-Proof]].
