# FUSE

Physics merge game where any two things can fuse. New combinations are invented once
by Claude on the server and the first player to make one gets their name on it.

- Client: this folder (`index.html`, single file, Matter.js from cdnjs)
- API: `hsnapi` → `src/projects/fuse` (mounted at `/api/fuse`)

## Run locally

1. API (from `D:\new project\hsnapi`), with a real key or the mock:

   ```bash
   ANTHROPIC_API_KEY=sk-ant-... DB_ENV=local node src/index.js
   ```
   or `FUSE_MOCK_AI=1 DB_ENV=local node src/index.js` to fake results.

2. Game (from this folder):

   ```bash
   node serve.js 5500
   ```
   Open http://localhost:5500/?api=http://localhost:3001/api/fuse (config.js points at production).
   Port 5500 is already in hsnapi's default CORS list.

`config.js` sets the API URL (`window.FUSE_API`). Override per visit with `?api=https://host/api/fuse`.
Without a reachable API the game still runs on the built-in starter tree.

## Deploy

- Game: upload `index.html` and `config.js` to https://fuse.aihunar.com (config.js already points at https://api.hsntech.in/api/fuse).
- API (api.hsntech.in): set `ANTHROPIC_API_KEY`, add `https://fuse.aihunar.com` to `ALLOWED_ORIGINS`,
  and set `FUSE_PROD_DB_NAME`, `FUSE_PROD_DB_USER`, `FUSE_PROD_DB_PASS` for the FUSE MySQL database
  (host, port and dialect fall back to the HSNWEB_PROD_DB_* values, same Hostinger account).
