# ecosystem.git

**Remote:** `https://github.com/AynBeirut/ecosystem.git`  
**Local (typical):** `~/Documents/grabio space/the eco sys/` (gitignored in grabio.space)  
**Also:** clone as sibling `~/Documents/ecosystem/` if preferred

## What lives here

| Path (under `the eco sys/`) | Contents |
|-----------------------------|----------|
| `finance/beirut-finance-flow-main/` | Invoice Manager SPA — embedded in Grabio admin |
| `finance/twa/` | Android TWA shell for Play Store |
| `ecosystem-plan/posfinal-main/` | Windows Electron POS (`pos-v1/`) |
| `ecosystem-plan/pos-windows-builder-pack/` | POS handoff docs, API contract |
| `obsidian/` | Legacy project-docs templates |
| `publish-insight/`, etc. | Other module sources |

## Why separate from grabio.space

- Large trees, binaries, module-specific release cycles
- POS/finance can ship on their own schedule
- Prevents PR boundary violations (see [[Decision-Log/2026-07-09-repo-boundary-split]])

## Remote branches (2026-07-09)

| Branch | Commit | Notes |
|--------|--------|-------|
| `feat/ecosystem-modular-local` | `baeb01b` | Full snapshot incl. 521 `the eco sys/` paths |
| `main` | `8a0c200` | 421 eco sys files |

## How grabio.space consumes it

1. **Finance embed** — Vite alias reads `the eco sys/finance/beirut-finance-flow-main/src`
2. **`npm run build:invoice`** — builds finance app, copies to `dist/invoice/`
3. **POS** — Windows app pairs via Grabio API; installer in Firebase Storage `pos/`

## Clone for fresh machine

```bash
cd ~/Documents
git clone https://github.com/AynBeirut/ecosystem.git
# Option A: symlink into grabio space
ln -s ~/Documents/ecosystem/the\ eco\ sys ~/Documents/grabio\ space/the\ eco\ sys
# Option B: checkout ecosystem branch into expected path
```

See [[Gotchas/Fresh-Clone]].
