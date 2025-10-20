## Copilot instructions — Hestia Cam (concise)

Goal: make small, safe edits that keep the PWA installable and the PeerJS client/server in sync.

Architecture (short)
- Frontend: `hestia-cam-main/` — static PWA, deploy to Netlify. Key: `index.html`, `sw.js`, `manifest.json`, `netlify/functions/peer-host.js`.
- Backend: `hestia-cam-server/` — Node PeerJS signalling server (Render). Key: `server.js`, `package.json`.
- Runtime: client connects to `wss://<PEER_HOST>/peerjs/myapp`; `PEER_HOST` is provided at runtime via the Netlify function.

Quick dev & deploy commands
- Frontend (local quick test): `cd hestia-cam-main && python -m http.server 8000` (HTTPS required for camera). Use ngrok or Netlify for full tests.
- Backend (local): `cd hestia-cam-server && npm install && node server.js`.
- Deploy: Netlify base dir `hestia-cam/hestia-cam-main` (publish `.`). Render root `hestia-cam/hestia-cam-server` (build `npm install`, start `npm start`).

Patterns & integration points
- Runtime-config: frontend fetches `/.netlify/functions/peer-host` → sets `window.__PEER_HOST` (preferred over hardcoding).
- SW: network-first for navigation, cache-first for assets; include `/offline.html` and icons in precache.
- PeerJS: server mount and client `path` must match exactly (`/peerjs/myapp`).

What to check before PR
- Ensure `PEER_OPTIONS.host/port/secure` derive from `window.__PEER_HOST` or `location.hostname`.
- Confirm manifest icons exist at `/icons/` (192/512) and are referenced by `manifest.json`.
- Verify service worker scope and that `/offline.html` is cached.

Files to open first: `index.html`, `sw.js`, `manifest.json`, `netlify/functions/peer-host.js`, `server.js`, `package.json`.

PR style
- Small, scoped commits. Default to non-breaking runtime flags and preserve mobile attributes (`playsinline`, `autoplay`).

If you want broader changes (CI, deploy automation, TWA packaging), ask and I will prepare a focused PR with tests and docs.
## Hestia Cam — Copilot instructions (short and actionable)

This file gives focused guidance so an AI coding agent can be immediately productive in this repository.

Keep instructions short: prefer concrete edits, small patches, and tests. When in doubt, open the files named below before editing.

---

1) Big picture / architecture
- Monorepo with two primary components:
  - `hestia-cam-main/` — frontend PWA (static site). Deploy to Netlify. Key files: `index.html`, `sw.js`, `manifest.json`, `netlify/functions/peer-host.js`, `netlify.toml`.
  - `hestia-cam-server/` — Node.js PeerJS signalling server. Deploy to Render. Key files: `server.js`, `package.json`.
- Runtime communication: frontend uses PeerJS connecting to `wss://<PEER_HOST>/peerjs/myapp`. The frontend reads `PEER_HOST` at runtime from a Netlify Function (`/.netlify/functions/peer-host`).

Why this matters: changes to `PEER_OPTIONS` in `index.html` must match the server mount path in `server.js` and the Render domain configured as `PEER_HOST` on Netlify.

2) Developer workflows (explicit commands)
- Local frontend quick serve (no HTTPS):
  - `cd hestia-cam-main && python -m http.server 8000`
  - Note: camera & installs require HTTPS — use ngrok or deploy to Netlify for full testing.
- Local backend (PeerJS) dev:
  - `cd hestia-cam-server && npm install && node server.js`
- Deploy:
  - Netlify: Base dir `hestia-cam/hestia-cam-main`, publish `.`. Set env var `PEER_HOST` to your Render domain.
  - Render: Root dir `hestia-cam/hestia-cam-server`, build `npm install`, start `npm start`.

3) Project-specific conventions & patterns
- Runtime-config pattern: the frontend fetches `/.netlify/functions/peer-host` to set `window.__PEER_HOST`. Prefer this runtime env approach instead of hardcoding hostnames in `index.html`.
- Service worker: `sw.js` uses network-first for navigation and cache-first for static assets. Keep offline fallback at `/offline.html` and precache icons referenced by `manifest.json`.
- CDN fallbacks: `index.html` attempts CDN scripts and falls back to local `/cdn/` copies if loading fails — preserve that pattern when adding external libs.
- PeerJS mounting: server code mounts `ExpressPeerServer` at `/peerjs` with path `/peerjs/myapp`. Any client `path` must match exactly.

4) Integration points & external dependencies
- PeerJS signalling server (package `peer`) — ensure `package.json` `peer` version aligns with client PeerJS version. Server uses `proxied: true` to respect TLS/proxy headers.
- TURN/STUN servers: repo includes openrelay as fallbacks. If connections fail behind strict NAT, add a paid TURN server.
- Netlify Functions: `netlify/functions/peer-host.js` returns the runtime `PEER_HOST` env var. Keep function path unchanged.

5) Typical small fixes the agent will perform
- Update `PEER_OPTIONS` derivation in `index.html` to use `window.__PEER_HOST` or `location.hostname` and set `secure` based on `location.protocol`.
- Improve `sw.js` caching rules (precaching offline page + assets). Add `/offline.html` to repo.
- Add or update `netlify.toml` headers for caching and security (already present; follow its patterns).

6) What to check before submitting a PR
- Ensure client/server `path` and `host` agree (client `PEER_OPTIONS.path === '/peerjs/myapp'` and server mounts at `/peerjs` with same internal path).
- Ensure manifest icons exist at `/icons/` and are referenced in `manifest.json`.
- Test basic flow locally or via staging deploy: Frontend (Netlify) served over HTTPS, backend (Render) available over HTTPS, Netlify env `PEER_HOST` set to Render domain.
- Run a quick manual smoke test: open site → Start Camera → Share → ensure peer id appears and wss connection to `wss://<PEER_HOST>/peerjs/myapp` succeeds.

7) Files worth opening first when asked to modify behavior
- `hestia-cam-main/index.html` — UI, PeerJS client options, SW registration
- `hestia-cam-main/sw.js` — service worker caching & offline behavior
- `hestia-cam-main/manifest.json` — icons/metadata for PWA
- `hestia-cam-main/netlify/functions/peer-host.js` — runtime host provider
- `hestia-cam-server/server.js` — PeerJS server mount, CORS
- `hestia-cam-server/package.json` — node engines & dependency versions

8) PR etiquette & safe defaults for agents
- Make minimal, scoped changes. Prefer adding feature flags or env-driven behavior rather than breaking changes.
- When adding runtime config, default to `location.hostname` so the site still works locally without env vars.
- Preserve existing UX: don't remove `playsinline`, `autoplay` attributes — they're intentional for mobile iOS behavior.

---

If anything above is unclear or you want this more opinionated (e.g., automated deploy CI), tell me which area to expand and I'll update this file.
