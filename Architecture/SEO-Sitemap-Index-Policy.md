# SEO Sitemap and Index Policy

Updated: 2026-09-10 (evening)

Grabio SEO Phase 2 prioritizes crawl correctness before scaling URL count. The 2026-09-10 GSC baseline for `https://grabio.space/` showed 16 indexed URLs, 3 not indexed URLs, and `/sitemap.xml` successfully submitted with 48 discovered pages. Evening deploy added **Internal Demo OS** URLs (`/demo-os`, `/demo-os/{module}`) and mock preview URLs (`/demo/*/app`, `/features/*/app`) to `platformSitemapUrls.ts` — re-export GSC after crawl.

## Sitemap Model

- `/sitemap.xml` is the stable sitemap index.
- `/sitemap-static.xml` is generated at build time from `functions/src/lib/platformSitemapUrls.ts`.
- `/sitemap-programmatic.xml` is served by the Functions API and includes only published `/pages/*` records passing quality gates.
- `/sitemap-stores.xml` is served by the Functions API and includes only online, non-test, indexable stores with brand/content signals.
- `/sitemap-products.xml` is served by the Functions API and includes only products from eligible stores with slug, image, description, price, and visible availability.

## Index Policy

Do not index protected or low-value utility routes: admin, auth, cart, favorites, orders, payment, profile, subscription, onboarding, builder, freelancer, team, invoice, upgrade, tracking, and 404 pages.

Do index public marketing, solution, blog, reviewed programmatic, eligible store, eligible product pages, and curated **demo-os** / **demo preview** routes (`/demo-os/*`, `/demo/*/app`, `/features/*/app`, `/demo/*/os/*` vertical tours are indexable when linked from marketing; vertical `/demo/*/os/*` not all in static sitemap yet).

## Open Risk

Store and product sitemap URLs use canonical store subdomains (`https://{slug}.grabio.space`). Full GSC reporting may require a Domain property for `grabio.space`, not only the apex URL-prefix property.
