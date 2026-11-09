# RyuLong-DEV

Controller repo for the RyuLong multi-repository project. It holds no
application code — only the VS Code workspace, the setup script, and the
gitignore rules that keep the 7 real repos out of this one's history.

## Layout

```
RyuLong-DEV/
├── RyuLong.code-workspace   # multi-root workspace (relative paths, safe to move)
├── scripts/setup.ps1       # clone whichever child repos are missing + npm install
├── RyuLong-APP/
├── RyuLong-SDB/
├── RyuLong-TRX/
├── RyuLong-EXE/
├── RyuLong-PWA/
├── RyuLong-PKG/
├── RyuLong-WEB/
```

Each `RyuLong-*` folder is its own git repository (own `.git`, own GitHub
remote under `ZYDRAXYL/`). `.gitignore` excludes them entirely from this repo.

## Chained repositories

From [`RyuLong-APP/chain/chain.json`](https://github.com/ZYDRAXYL/RyuLong-APP/blob/main/chain/chain.json):

| Repo | Role | Owns | Releases | Visibility |
|---|---|---|---|---|
| [RyuLong-APP](https://github.com/ZYDRAXYL/RyuLong-APP) | hub | `.claude/`, `chain/`, `docs/`, `process/`, `tools/` | — | private |
| [RyuLong-SDB](https://github.com/ZYDRAXYL/RyuLong-SDB) | schema | `schema/`, `supabase/`, `assets/`, `generated/` | `sdb-v*` | public |
| [RyuLong-TRX](https://github.com/ZYDRAXYL/RyuLong-TRX) | service | `netlify/`, `public/`, `netlify.toml` | — | public |
| [RyuLong-EXE](https://github.com/ZYDRAXYL/RyuLong-EXE) | app | `electron/` | `v*` | private |
| [RyuLong-PWA](https://github.com/ZYDRAXYL/RyuLong-PWA) | build | `tools/`, `shim/`, `dist/` | — | public |
| [RyuLong-PKG](https://github.com/ZYDRAXYL/RyuLong-PKG) | content | `packages/`, `index.json` | `pkg-v*` | public |
| [RyuLong-WEB](https://github.com/ZYDRAXYL/RyuLong-WEB) | site | `*.html`, `assets/` | `mirror` | public |

Changes flow one way along the chain:

```
EXE    APP > SDB, TRX > EXE > PKG, WEB, PWA
PWA    APP > SDB, TRX > EXE > PWA > WEB
```

## First-time setup on a new device

Prerequisites: [Git](https://git-scm.com/) with access to the `ZYDRAXYL` org (APP, EXE are private), and [Node.js LTS](https://nodejs.org/).

```powershell
git clone https://github.com/ZYDRAXYL/RyuLong-DEV.git
cd RyuLong-DEV
./scripts/setup.ps1
```

Then open `RyuLong.code-workspace` in VS Code.

> If PowerShell refuses to run the script, run it once as:
> `powershell -ExecutionPolicy Bypass -File .scriptssetup.ps1`

## License

MIT — see [LICENSE](LICENSE). Created by LDKTC.
