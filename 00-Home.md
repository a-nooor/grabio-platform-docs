# Grabio Platform — Home

> **Single source of truth.** Code-repo `backlog.md` and scattered `docs/` files are stubs or archives — update here first.

## Quick links

| Section | Purpose |
|---------|---------|
| [[Architecture/Overview]] | What exists today, per repo |
| [[Architecture/Repo-Boundaries]] | What must never cross repos |
| [[Backlog/Open]] | Open work only (repo-synced) |
| [[Deploy/Protocol]] | Non-negotiable deploy gates |
| [[Gotchas/Index]] | Symptom → fix lookup |

## Repos (local layout)

```text
~/Documents/
├── grabio space/              ← grabio.space (main app)
├── grabio-platform-docs/      ← this vault
├── ecosystem/                 ← optional clone of ecosystem.git
└── grabio space/the eco sys/  ← gitignored in grabio.space; from ecosystem.git
```

## Remotes

| Name | Remote | Default branch |
|------|--------|----------------|
| Main app | `origin` → `github.com/AynBeirut/grabio.space` | `main` |
| Ecosystem | `ecosystem` → `github.com/AynBeirut/ecosystem` | `main` |
| Supabase copy | nested `.git` in `suba eco sys/` | local |

## Firebase production

- **Project:** `market-flow-7b074`
- **Hosting:** grabio.space
- **API:** Cloud Run `api-5nbn2jdbxa-uc.a.run.app` (via functions deploy)

## Session checklist (before done)

- [ ] Decision made? → [[Decision-Log/_template|new Decision-Log entry]]
- [ ] Blocker opened/closed? → [[Backlog/Open]]
- [ ] New gotcha? → [[Gotchas/Index]]
- [ ] Architecture changed? → relevant `Architecture/*` note
