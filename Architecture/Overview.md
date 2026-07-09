# Architecture — Overview

**Last updated:** 2026-07-09

## System diagram (current state)

```mermaid
flowchart TB
  subgraph grabio_space ["grabio.space"]
    WEB[React SPA / Admin]
    FN[Cloud Functions API]
    FS[(Firestore)]
    ST[Firebase Storage]
  end

  subgraph ecosystem_git ["ecosystem.git (local: the eco sys/)"]
    FIN[beirut-finance-flow-main]
    POS[posfinal-main / Windows POS]
    PLAN[ecosystem-plan / builder packs]
  end

  subgraph suba ["suba eco sys (Supabase copy)"]
    SUPA[grabio-platform + Edge Functions]
    PG[(Supabase Postgres)]
  end

  WEB -->|embed alias| FIN
  WEB --> FN
  FN --> FS
  POS -->|pairing + sync API| FN
  FIN -->|build:invoice → dist/invoice| WEB
  SUPA -.->|parallel test stack grabio.online| PG
```

## Per-repo summary

| Repo | [[Architecture/grabio.space|grabio.space]] | [[Architecture/ecosystem.git|ecosystem.git]] | [[Architecture/suba-eco-sys|suba eco sys]] |
|------|-------------|----------------|--------------|
| **Purpose** | Production platform (hosting, rules, API, admin) | Module source trees (finance, POS, plans) | Firebase→Supabase experiment |
| **Deploy target** | Firebase prod | Build artifacts consumed by main app; POS installer to Storage | grabio.online test only |
| **In grabio.space git?** | Yes (this repo) | **No** — gitignored; clone separately | **No** — separate nested repo |
| **Status** | PR #1 open (`feat/ecosystem-modular-local`) | `feat/ecosystem-modular-local` @ `baeb01b` has full eco tree | Schema migrated; R2 keys pending |

## Integration touchpoints

See [[Architecture/Integration-Map]].

## Hard boundaries

See [[Architecture/Repo-Boundaries]] — violated once in PR #1 (fixed 2026-07-09).
