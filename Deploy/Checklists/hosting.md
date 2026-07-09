# Checklist — Hosting

## Pre-deploy

- [ ] Owner approved deploy ([[Deploy/Protocol]])
- [ ] `npm run build` succeeds locally (includes `build:invoice` if finance changed)
- [ ] No unintended `.env.production` changes in commit
- [ ] PR boundary check passed (no `the eco sys/` in grabio.space)

## Deploy

```bash
cd ~/Documents/grabio\ space
npm run build
firebase deploy --only hosting
```

## Post-deploy proof

- [ ] New JS bundle hashes in `dist/` / Network tab (not old `AdminProducts-*.js` etc.)
- [ ] `/admin` loads for test account
- [ ] `/invoice/` loads if finance artifact shipped
- [ ] Service worker: bump or verify cache invalidation if admin behaved stale before

## Rollback

- Redeploy previous hosting version from Firebase Console → Hosting → Release history
- Or: `git checkout <prev>` → build → deploy
