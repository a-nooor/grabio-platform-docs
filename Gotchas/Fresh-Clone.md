# Gotchas — Fresh Clone

**Last updated:** 2026-07-09

## Minimum clones

```bash
# 1. Main app
git clone https://github.com/AynBeirut/grabio.space.git ~/Documents/grabio\ space
cd ~/Documents/grabio\ space
git checkout feat/ecosystem-modular-local   # or main after PR merge

# 2. Ecosystem (finance + POS source) — REQUIRED for build
git clone https://github.com/AynBeirut/ecosystem.git ~/Documents/ecosystem
git -C ~/Documents/ecosystem checkout feat/ecosystem-modular-local

# 3. Place finance tree where grabio.space expects it
ln -sfn ~/Documents/ecosystem/the\ eco\ sys ~/Documents/grabio\ space/the\ eco\ sys
```

## Docs vault

```bash
git clone <grabio-platform-docs-remote> ~/Documents/grabio-platform-docs
# Or use local copy created 2026-07-09; push remote when ready
```

Open `grabio-platform-docs` in Obsidian.

## Environment files (not in git)

| File | Purpose |
|------|---------|
| `.env.production` | Vite production vars |
| `.env.local` | Local feature flags (optional) |
| `.credentials.md` | All secrets — **never commit** |

Copy from team secure store or `.env.local.example` in repo.

## Install & run

```bash
cd ~/Documents/grabio\ space
npm install
npm run dev    # http://localhost:8080
```

## Verify build

```bash
npm run build
ls dist/invoice/index.html    # finance artifact
```

## Firebase CLI

```bash
npm install -g firebase-tools
firebase login
firebase use market-flow-7b074
```

## Optional: Supabase copy

Only if working on grabio.online:

```bash
cd ~/Documents/grabio\ space/suba\ eco\ sys/grabio-platform
cp .env.example .env
npm install && npm run dev
```

## Cursor rules sync

```bash
scripts/obsidian/sync-cursor-config.sh /path/to/grabio-ai-core
```

See `suba eco sys/obsidian/README.md` for global AI core layout.
