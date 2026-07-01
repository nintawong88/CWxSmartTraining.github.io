# AGENTS.md

## Cursor Cloud specific instructions

### What this is
Client-side only static web app: **CWx StockTake Roster App** (bilingual EN/TH). There is no backend, no build step, and no package manager — the repo is a set of standalone `.html` files. All app state is persisted in the browser via `localStorage` (key `cwx_roster_state`), seeded from an inline `seedData` object.

- `index.html` (and identical `Index.html`) — the main single-page application.
- `CWx_Count_Plan_Roster_July2026.html`, `counter_guide.html`, `manual.html` — auxiliary/reference pages.

### Running it
Serve the repo root over HTTP and open `index.html`; do not open via `file://` (relative paths and some browser behaviors expect an HTTP origin). Example: `python3 -m http.server 8000` from the repo root, then browse to `http://localhost:8000/index.html`.

### Non-obvious caveats
- Tailwind CSS and the XLSX library load from public CDNs (`cdn.tailwindcss.com`, `cdnjs.cloudflare.com`). **Internet access is required in the browser** for styling and Excel import/export to work.
- Default seeded logins (from `seedData.users`): `admin` / `123456!` (role `admin`, sees User Management) and `PIC_user` / `123456!`.
- State lives in `localStorage`; to reset the app to seed data, clear site data / `localStorage` for the origin. Changes made in the UI are only saved to that browser profile.
- `index.html` and `Index.html` are byte-identical duplicates (case-only difference); edit both if changing app behavior.
- There is no lint/test/build tooling in this repo.
