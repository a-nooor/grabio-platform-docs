# Checklist — Firestore Rules

## Pre-deploy

- [ ] `npm run test:firestore-rules` passes (emulator)
- [ ] Review diff for accidental broad `allow read, write: if true`
- [ ] Indexes updated in `firestore.indexes.json` if new queries added

## Deploy

```bash
firebase deploy --only firestore:rules
firebase deploy --only firestore:indexes   # if changed
```

## Post-deploy proof

- [ ] Test with real user token on affected collection (e.g. `finishedGoodsInventory`, `recipes`, POS device paths)
- [ ] Admin page that previously failed now loads without permission-denied

## Common failure mode

Rules deployed but **client still uses old cached bundle** that queries before `waitForAuthToken` — fix in app + hosting deploy, not rules alone.
