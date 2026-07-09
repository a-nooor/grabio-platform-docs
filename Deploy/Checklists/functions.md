# Checklist — Functions

## Pre-deploy

- [ ] `npm run build --prefix functions` succeeds
- [ ] storeCommerceGuard tests if guard touched: `node scripts/testStoreCommerceGuard.cjs`
- [ ] Owner approval ([[Deploy/Protocol]])

## Deploy

```bash
firebase deploy --only functions
```

## Post-deploy proof

- [ ] Health endpoint returns expected version string
- [ ] Changed route tested (checkout, POS, subscription, etc.)
- [ ] No spike in Cloud Run errors (Firebase Console → Functions → Logs)

## POS-specific

- [ ] `GET /pos/catalog` with valid device token
- [ ] Pairing flow from [[Architecture/Integration-Map#POS (Windows)]]

## Rollback

- Firebase Console → Functions → previous revision
- Or redeploy from known-good git tag
