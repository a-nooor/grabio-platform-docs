# Runtime Proof

What counts as evidence that a change works in **production or realistic staging**.

## Principles

1. **Exercise the changed path** — not just "server starts"
2. **Use real auth** when rules or guards changed — test store with known tier/demo flag
3. **Record command + output** in session notes or [[Decision-Log/_template|Decision-Log]] if non-obvious

## Examples (grabio.space)

### storeCommerceGuard

```bash
node scripts/testStoreCommerceGuard.cjs
# Expect: pass/fail cases for demo, inactive, active stores
```

### Firestore rules

```bash
npm run test:firestore-rules
# Emulator-based; re-deploy rules before claiming prod parity
```

### POS API (post-deploy)

```bash
curl -s "https://api-5nbn2jdbxa-uc.a.run.app/health"
# Version string should match deployed functions
```

Pairing/catalog require device token — test via admin UI + paired device or audit script:

```bash
node functions/scripts/audit-pos-devices.mjs
```

### AdminProducts permission fix

1. Deploy hosting with new bundle hash
2. Login as test merchant (`anwar.abouhassan@gmail.com` / store `E-Service`)
3. Open `/admin/products` — no Firestore permission-denied in console
4. If old bundle filename appears in Network tab → SW/cache issue ([[Gotchas/Index]])

### Invoice embed

```bash
npm run build
test -f dist/invoice/index.html && echo OK
```

Then browser: `/admin/finance/invoices` inside admin chrome, same session as main app.

## What to document after proof

- Date, environment (local / staging / prod)
- Commit or deploy version
- Link to [[Backlog/Done]] when closing related open item
