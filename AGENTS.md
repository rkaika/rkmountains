# Agent Instructions

This repository is a small static site for mountaineering planning. Treat it as a plain HTML/CSS/JavaScript project: there is no build step, package manager, or framework.

## Repository Map

- `index.html` is the home page. It links to the weather dashboard and field guides.
- `mw.html` is the current production weather dashboard.
- `climb.html` is the Summit-Day Check, a lightweight during-climb page. Its `PEAKS` data is a trimmed copy of `MTNS` in `mw.html`; keep keys, slugs, coordinates, and thresholds in sync when objectives change.
- `mw3.html`, `mw2.html`, and `mw1.html` are older or experimental dashboard copies. Do not edit them unless the task explicitly asks for it.
- `mount-baker-easton.html` and `mount-whitney-main-trail.html` are standalone field guides.
- `assets/baker-easton/` and `assets/whitney-main-trail/` contain local guide images.
- `mountain-weather-window.html` is an earlier prototype kept for reference.
- `README.md` documents user-facing behavior, supported objectives/routes, and file inventory.

## General Editing Rules

- Keep changes scoped to the requested behavior. Avoid broad refactors of the large standalone HTML files.
- Preserve the existing no-build static-site style. Use inline CSS and inline JavaScript when extending existing pages.
- Prefer ASCII in new text unless editing nearby content that already uses specific symbols or route names.
- Do not remove or rewrite user work. Check `git status --short` before staging or committing.
- Do not commit unless the user asks. When committing, stage only intended paths.

## Weather Dashboard Changes

Most dashboard data lives in `mw.html`:

- `const MTNS` defines objectives, summit coordinates, NWS office, thresholds, routes, route slugs, trailhead coordinates, route aspects, mileage, AllTrails links, and optional `profilePoints`.
- `const MTN_LINKS` defines companion quick links for each objective.
- `initForm()` controls dropdown grouping. Washington objectives should be included in `WA_KEYS` so they appear above the separator.
- URL sharing uses `m` for the `MTNS` key and `r` for a route slug. Keep slugs stable once published.

When adding or changing objectives/routes:

- Update `MTNS` and, when applicable, `MTN_LINKS`.
- Add route `profilePoints` when useful for route profile weather.
- Verify NWS office IDs from `api.weather.gov/points/{lat},{lon}` when adding new summit points.
- Update `README.md` supported objective and route tables.
- If the objective has or needs a field guide, update `index.html` and the README file inventory.

## Field Guide Changes

Field guides are standalone HTML pages modeled after `mount-baker-easton.html`:

- Keep the first screen as an actual route guide, not a marketing landing page.
- Use local assets under `assets/<route-name>/`; avoid relying on hotlinked images for normal page rendering.
- Include official source links for permits, land managers, weather, and route context where possible.
- Make route-scope explicit when routes have similar names or nearby alternatives.
- After adding a guide, add a card to the Field Guides section in `index.html` and update `README.md`.

## Validation

For small content-only docs changes:

```sh
git diff --check -- README.md AGENTS.md
```

For `mw.html` JavaScript edits, parse inline scripts before finishing:

```sh
node -e 'const fs=require("fs"); const html=fs.readFileSync("mw.html","utf8"); const scripts=[...html.matchAll(/<script>([\s\S]*?)<\/script>/g)].map(m=>m[1]).join("\n"); new Function(scripts); console.log("script parse ok");'
```

For pages with changed UI or images:

```sh
python3 -m http.server 8766
```

Then open `http://localhost:8766/` or the changed page and check desktop and mobile widths for:

- no horizontal overflow
- images loading
- navigation links working
- text not overlapping

Stop any temporary server you start before finishing.

## Git Hygiene

- Always inspect `git status --short` before staging.
- If unrelated files are modified, leave them alone.
- Stage exact intended paths, for example:

```sh
git add README.md
git add index.html mount-whitney-main-trail.html assets/whitney-main-trail
```

- Use concise commit messages that describe the user-facing change.
