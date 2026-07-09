# 2026-07-09 — Repo boundary split (eco sys out of grabio.space)

**Context:** PR #1 (`feat/ecosystem-modular-local`) contained ~455 files under `the eco sys/`, violating the platform vs ecosystem separation.

**Decision:**
- Strip `the eco sys/`, `LINUX-BUILDER-PROMPT.md`, `pos-client/` from grabio.space history via `git filter-repo`
- Add `the eco sys/` to `.gitignore` in grabio.space
- Push full pre-strip snapshot to `ecosystem.git` branch `feat/ecosystem-modular-local` @ `baeb01b`
- **Do not merge PR #1** until boundary confirmed (done for eco paths; merge still pending owner review)

**Rejected alternatives:**
- Keep eco sys in grabio.space for "convenience" — bloated repo, wrong ownership, repeat of binary/history issues
- Submodule without team agreement — deferred; disk checkout + ecosystem.git for now

**Consequences:**
- Fresh `git clone grabio.space` does **not** include finance source — must clone ecosystem.git separately ([[Gotchas/Fresh-Clone]])
- `npm run build` fails without local `the eco sys/finance/...` path
- Local disk folder (~3.4G) remains; untracked in grabio.space

**Repos affected:** grabio.space, ecosystem.git

**Links:** https://github.com/AynBeirut/grabio.space/pull/1
