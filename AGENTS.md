# AGENTS.md

## Cursor Cloud specific instructions

### What this project is
This repo is a **fully static, client-side web app** (no backend, no build step, no
package manager). The product is the **CWx StockTake Roster App** — a single-page app
for managing stock-take counting teams, rosters, employees and locations. State is
persisted entirely in the browser via `localStorage` (key `cwx_roster_state`).

Key files:
- `index.html` — the main application (single-file SPA; ~19.5k lines). `Index.html` is an
  identical duplicate. The app loads Tailwind and SheetJS (`xlsx`) from CDNs, so an
  internet connection is needed for full styling/Excel export.
- `manual.html`, `counter_guide.html`, `CWx_Count_Plan_Roster_July2026.html` — standalone
  static documents (Thai-language user guide / printable roster), openable directly.

### Running the app (dev)
There is nothing to install or build. Serve the static files over HTTP (opening via
`file://` works for basic use but HTTP avoids browser quirks):

```
python3 -m http.server 8000
```

Then open `http://localhost:8000/index.html`.

- Default login (seeded in `seedData` inside `index.html`): username `admin`,
  password `123456!` (admin role). A second seeded user is `PIC_user` / `123456!`.
- The "User Management" sidebar item only appears for the `admin` role.

### Gotchas
- All persistence is `localStorage`; there is **no server/database**. To reset to seed
  data, use the "Reset App Data" link on the login screen (or clear site data /
  `localStorage.removeItem('cwx_roster_state')`).
- Because Tailwind/`xlsx` come from CDNs, with no network the page renders unstyled and
  the Excel import/export features will not work.

### Lint / Test / Build
There is **no** lint, test, or build tooling in this repo (no `package.json`, no config).
Verification is manual: serve the files and exercise the UI in a browser.
