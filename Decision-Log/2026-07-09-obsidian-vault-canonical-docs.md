# 2026-07-09 — Obsidian vault as canonical docs

**Context:** Documentation scattered across `backlog.md` (1000+ lines), `docs/`, eco sys templates, and chat history.

**Decision:**
- Create separate vault `~/Documents/grabio-platform-docs/` (Option A)
- Sections: Architecture, Decision-Log, Backlog, Deploy, Gotchas
- Code-repo `backlog.md` and deployment checklists become **stubs** pointing here
- Update vault **before** marking any session done (not a separate pass at end)

**Rejected alternatives:**
- `docs/vault/` inside grabio.space — crosses repo boundary for ecosystem/supabase docs
- Vault only in ecosystem.git — deploy rules belong with platform ownership
- Keep maintaining dual backlog.md + vault — rejected (single source of truth)

**Consequences:**
- Agents and devs open Obsidian vault alongside code
- Legacy `backlog.md` archived at [[Backlog/archive/README]]; open items only in [[Backlog/Open]]

**Repos affected:** grabio-platform-docs (new), grabio.space (stubs only)
