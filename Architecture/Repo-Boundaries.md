# Repo Boundaries

**Last updated:** 2026-07-09  
**Severity:** Non-negotiable

## Policy

| Repo | Owns | Must NOT contain |
|------|------|------------------|
| **grabio.space** | Platform: hosting, rules, API, admin UI, embed *wiring* | `the eco sys/` source trees, POS/finance app source, ecosystem binaries |
| **ecosystem.git** | Module sources: finance, POS, plans, obsidian templates | Production deploy configs for grabio.space (except handoff docs) |
| **suba eco sys** | Supabase experiment | Production Firebase deploys; must not replace `the eco sys/` |

## Violation example (fixed)

PR #1 originally included ~455 files under `the eco sys/`. Stripped via `git filter-repo` before merge. Ecosystem content preserved on `ecosystem.git` @ `baeb01b`.

## Allowed cross-repo references (grabio.space)

- **Disk path imports** in `vite.config.ts` — finance on local filesystem (gitignored)
- **API contracts** in `docs/planning/pos-*.md`
- **Scripts** that assume sibling checkout — document in [[Gotchas/Build-Dependencies]]

## Forbidden

- Committing `the eco sys/` into grabio.space
- Merging ecosystem-only PRs into grabio.space without boundary review
- Credentials in any repo (use `.credentials.md` local only)

## Before any PR merge

1. `git diff main...HEAD --name-only | grep "the eco sys"` → must be empty
2. Confirm ecosystem.git has module changes if eco work was done
3. Update [[Backlog/Open]] and [[Decision-Log/_template|Decision-Log]] if boundary-related
