# Hermes Desktop

A desktop-only view of [Hermes Agent](https://github.com/NousResearch/hermes-agent), tracking only the Electron desktop app and its shared workspace package.

## What’s in this repo

- `apps/desktop/` — the full Electron desktop shell (React + Vite + Node 22 + node-pty)
- `apps/shared/` — tiny `@hermes/shared` TypeScript package used by the desktop workspace

Nothing else. No Python backend, no gateway, no TUI, no Docker.

## Upstream sync

This branch is regenerated from upstream as:

```
git-filter-repo --path apps/desktop --path apps/shared
```

Because of that, direct merges from the full upstream repo will reintroduce the entire monorepo. Do **not** use GitHub’s “Sync” button.

### Automatic sync

A GitHub Actions workflow runs once a day at 06:00 UTC. It:
1. fetches `NousResearch/hermes-agent` `main`
2. filters the tree to `apps/desktop/` + `apps/shared/`
3. force-pushes the filtered result back to this repo’s `main`

You can also trigger it manually from the **Actions** tab (`workflow_dispatch`).

### Manual sync

```bash
git fetch upstream
git checkout upstream/main
git checkout -b desktop-next
git filter-repo --path apps/desktop --path apps/shared --force
git checkout main
git merge --ff-only desktop-next
git branch -d desktop-next
git push origin main --force
```

## Local development

```bash
cd apps/desktop
npm install
npm run build      # or npm run dev
```

## Remotes

- `origin` → `https://github.com/PcRoGamer/hermes-desktop.git`
- `upstream` → `https://github.com/NousResearch/hermes-agent.git`
