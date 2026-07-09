# Gotchas — Build Dependencies

**Last updated:** 2026-07-09

## Finance embed (hard dependency)

grabio.space **does not** contain finance source in git. Build assumes on-disk path:

```text
the eco sys/finance/beirut-finance-flow-main/
```

### package.json

```json
"build": "vite build && npm run build:invoice",
"build:invoice": "npm run build --prefix \"the eco sys/finance/beirut-finance-flow-main\" && node scripts/copy-invoice-dist.cjs"
```

### vite.config.ts

```ts
const financeSrcPath = path.resolve(__dirname, "the eco sys/finance/beirut-finance-flow-main/src");
```

### Runtime imports

- `src/vite-finance-alias.ts` — dev/build alias
- `src/embed/financeFirebaseBridge.ts` — imports finance `embedBridge`
- `src/pages/admin/finance/financeEmbeddedLoaders.ts` — dynamic imports into finance pages

**CI implication:** Pipeline must checkout ecosystem.git into `the eco sys/` before `npm run build`, or split build jobs.

## Copy script

`scripts/copy-invoice-dist.cjs` copies finance `dist/` → `dist/invoice/` for hosting rewrite `/invoice/**`.

## firebase.json

Hosting rewrite serves embedded finance at `/invoice/` (TWA + standalone).

## tsconfig

`tsconfig.app.json` may reference finance paths — keep in sync when moving ecosystem checkout.

## POS (no compile-time dependency)

POS Windows app builds from ecosystem.git only. grabio.space provides API + Storage installer only.

## Mobile invoice

`grabio-mobile` uses gated screens; may expect `dist/invoice` deployed or WebView URL — verify parity script:

```bash
node grabio-mobile/scripts/verify-invoice-parity.mjs
```

## If build fails with ENOENT on finance path

1. Confirm symlink or folder exists: `ls "the eco sys/finance/beirut-finance-flow-main/package.json"`
2. Clone ecosystem.git — [[Gotchas/Fresh-Clone]]
3. Do **not** re-add finance to grabio.space git — [[Architecture/Repo-Boundaries]]
