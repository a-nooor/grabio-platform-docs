# Grabio Platform Docs (Obsidian vault)

**Canonical documentation** for the Grabio platform across all repos.

Open this folder as an Obsidian vault (`File → Open folder as vault`).

| Repo | Primary | Backup |
|------|---------|--------|
| Main app | `https://github.com/AynBeirut/grabio.space.git` | — |
| Ecosystem code | `https://github.com/AynBeirut/ecosystem.git` | `https://github.com/a-nooor/ecosystem.git` |
| **This vault (docs)** | `https://github.com/AynBeirut/grabio-platform-docs.git` | `https://github.com/a-nooor/grabio-platform-docs.git` |
| Supabase copy | `suba eco sys/` (nested git, local) | — |

**Dual push (required):** after every doc change, push to **both** accounts:

```bash
git push origin main && gh auth switch -u a-nooor && git push backup main && gh auth switch -u AynBeirut
```

Same rule applies to main code in `grabio space` — see that repo’s README.

**Entry point:** [[00-Home]]

**Developer landing map:** [[Architecture/Developer-Landing-Map]]

**Structure map:** [[Architecture/Packages-Workflows-Modules]]

**Fine-dining product map:** [[Architecture/Fine-Dining-Platform-Map]]

**Workspace policy:** [[Architecture/Workspace-Organization-Policy]]

**Setup separation:** [[Architecture/Setup-Surface-Separation]]

**Role policy:** [[Architecture/Role-Permission-Environment-Policy]]

**Resolver contracts:** [[Architecture/Resolver-Contracts]]

**No-risk accounting setup:** [[Runbooks/Client-Accounting-Setup-No-Risk]]

## Session rule

Before marking any task done: update Decision-Log, Backlog/Open, Gotchas, or Architecture as needed. No separate doc pass at the end.

## Platform change governance

Every client request or setup discovery must be classified before implementation:

- **Global platform fix:** shared behavior is wrong for every store.
- **Tenant option:** different stores can reasonably need different behavior.
- **Account data setup:** one store needs data/configuration using existing capabilities.
- **Temporary exception:** urgent blocker with owner approval and a documented removal path.

Default rule: tenant-specific workflow, UX, permissions, order statuses, reservations, advance ordering, payment methods, labels, mobile/POS behavior, and accounting behavior must become typed store settings with safe defaults. Web, POS, mobile, and Cloud Functions must read the same effective settings source.

Product direction rule: active roadmap energy goes to fine-dining restaurant daily operations plus CRM. Accounting/inventory/finance remain optional restaurant maturity modules. Builder/template/SEO/content stay connected inside Grabio as gated high-end client modules. NGO, freelancer, mini shop, publisher, and broad custom growth are deferred unless Anwar explicitly reopens them.

Setup rule: backend scripts, imports, and AI-assisted setup are starting methods only. Every store setup result must be visible in the admin UI, editable by the store user when allowed, and connected to the next setup step. Repeated setup work should become guided UI: template download, upload, validation preview, AI/setup correction, owner approval, and saved store data.
