# AGENTS.md

## Project overview
KRELUSMC is a **static single-page site** (Spanish-language Minecraft server community page). The entire app is `index.html` (HTML + inline CSS + vanilla JS) plus `logo.png`. There is no backend, no build step, and no package manager.

## Running it
- Served by `nginx:alpine` via `docker-compose.base44.yml`, bind-mounting the repo root to `/usr/share/nginx/html`.
- Web entry point is on host port **3000**.
- `nginx.base44.conf` runs the nginx worker as `root` because the sandbox repo root dir is mode `700` (the default `nginx` user cannot traverse it). Do not remove this override or you'll get 403.
- Edits to `index.html` are served immediately (no rebuild), but the browser won't auto-refresh — call `reload_preview` after edits so the user sees them.

## State / auth
- All client state lives in `localStorage` (`kmc_admin`, `ub_user`, `ub_msgs`).
- Admin login uses Google OAuth (`googleapis.com/oauth2/v3/userinfo`) — optional, no server or credentials required for the site to boot.

## Secrets
- None required to boot. No external service credentials needed.
