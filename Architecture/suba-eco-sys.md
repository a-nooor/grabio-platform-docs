# suba eco sys (Supabase copy)

**Local:** `~/Documents/grabio space/suba eco sys/`  
**Nested git:** yes — independent from grabio.space and ecosystem.git

## Purpose

Parallel **Firebase → Supabase** stack for **grabio.online** test domain. Not production.

## What lives here

| Path | Role |
|------|------|
| `grabio-platform/` | Vite frontend (Supabase client) |
| `scripts/` | Data migration Firebase → Supabase |
| `finance/` | Finance copy (relative paths vs `the eco sys/`) |
| Edge Functions | Deployed to Supabase (10 functions) |

## Status (2026-07-04)

| Item | State |
|------|-------|
| Schema migrations 1–5 | Done |
| Data migration (10 stores, 689 orders, …) | Done |
| Hosting grabio-online.web.app | Done |
| R2 image uploads | **Blocked** — Cloudflare R2 keys in Edge secrets |
| POS migration | Last — after Windows builder |

## Never rules

- Do **not** touch `the eco sys/` — live production source for Firebase stack
- Do **not** deploy `suba eco sys` to production until 1-week test passes
- Do **not** commit Supabase secrets to any repo

## Docs

- `suba eco sys/README.md` — quick start
- `suba eco sys/MIGRATION-PLAN.md` — full migration plan
- Open items: [[Backlog/Open#suba eco sys]]
