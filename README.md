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

## Session rule

Before marking any task done: update Decision-Log, Backlog/Open, Gotchas, or Architecture as needed. No separate doc pass at the end.
