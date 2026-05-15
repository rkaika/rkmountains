# RK Mountains

Small static mountaineering weather tool for comparing climb windows on west-coast and Alaska routes.

## Main Page

Open `mw.html` (or `index.html`, which redirects there) to use the mountaineering weather dashboard.

The page helps evaluate a selected mountain, trailhead/route, and climb window. It combines official NWS point forecasts with raw model guidance so you can compare the human-edited baseline against multiple numerical models.

## What Is On The Page

- **Mountain and route controls**: choose a peak, trailhead/route, climb start, and climb end. Washington peaks group at the top of the dropdown; others (OR/CA/AK) sit below a separator.
- **Crumb header**: name → route, trailhead elevation → summit elevation with computed gain, round-trip miles when known, and the selected climb window.
- **Selected climbing window group**: a visually grouped block for the core climb-window decision surfaces: verdict, summary metric cards, and route profile weather.
- **Climbing Window Guidance panel**: a Go / Watch / Caution verdict driven by wind, gust, and precipitation thresholds, followed by the sorted critical-criteria list (red → yellow → green) and a per-hour sparkline showing worst-of-three banding with P/W/G driver letters in cells that hit watch or caution.
- **Summary cards (met grid)**: summit temperature, trailhead temperature, upper-mountain peak wind, upper-mountain peak gust, freezing level, precipitation probability, snow signal, and model spread — laid out directly below the verdict.
- **Route profile weather**: NWS point forecasts for trailhead, curated route references, and summit/objective where available. Cards show point elevation, temperature range, precipitation probability, wind, gust when available, and snow signal. Points are planning anchors, not navigation data.
- **Route Weather Timeline**: a Mountain-Forecast-style timeline from 48 hours before the selected start through 12 hours after the selected end, sampled every 3 hours. It includes sky/precip signal, wind/gust/direction, precipitation probability and amount, model-grid temperature, wind chill, freezing level, and cloud cover. A selector switches the timeline between summit, route mid-point, and trailhead.
- **Hourly details**: collapsed by default; expands to hour-by-hour summit and trailhead temperatures alongside wind, gust, direction, freezing level, precipitation probability, sky cover, and notes.
- **Model charts**: Open-Meteo model comparison charts for wind, gusts, freezing level, precipitation probability, and snowfall. Charts show two days before the climb start through two days after the climb end, with the selected climb window highlighted.
- **Signal tiles**: Wet snow, Rain on snow, and Wind exposure cards with hover explanations and external reference links on the headline value.
- **External context**: NWS active alerts, regional avalanche forecast, and SNOTEL/NRCS snowpack pointers.
- **Recent precipitation**: recent model-mean precipitation totals at the summit. Climb-day civil light, sunrise/sunset, and moon illumination are shown compactly in the Climbing Window Guidance bullets.
- **Current observations**: nearby station observations, including elevation-aware notes where available.
- **Model guidance for this window**: lead-time-aware advice on which models to lean on (Nowcast / HRRR lead ≤48 h / NAM bridge ≤84 h / Global pattern beyond), updating based on the selected climb start.
- **Interpretation notes**: how to read the NWS baseline, when HRRR leads, how to cross-check globals against mesoscale, and what Model Spread means for confidence.
- **NWS Area Forecast Discussion**: the latest AFD for the relevant forecast office.
- **Dark/light mode**: toggle in the header; the preference is saved in the browser.

## Data Sources

- **Summit and trailhead temperatures**: NWS hourly point forecasts from `api.weather.gov`.
- **Snow signal**: NWS grid forecast data, including snowfall amount where available.
- **Wind, gusts, temperature, freezing level, precipitation, snowfall, and cloud cover**: Open-Meteo model data.
- **Route Weather Timeline and recent precipitation**: Open-Meteo model data using `past_days=3`, sampled around the selected climb window.
- **Forecast discussion**: NWS Area Forecast Discussion products from `api.weather.gov`.

Open-Meteo model comparisons currently include:

- GFS
- ECMWF IFS 0.25°
- DWD ICON
- Canadian GEM
- HRRR
- NAM

HRRR and NAM have shorter forecast horizons than the global models, so they only appear in the table/charts when data is available for the selected window.

## How To Use It

Use the hosted GitHub Pages version: [rkaika.github.io/rkmountains](https://rkaika.github.io/rkmountains/).

Then:

1. Select a mountain and route/trailhead.
2. Set your climb start and expected end time.
3. Click **Get Forecast**.
4. Read **Climbing Window Guidance** first, then scan the summary cards and route profile weather.
5. Use the **Route Weather Timeline** selector to compare summit, mid-point, and trailhead conditions before, during, and shortly after the climb. Open **Hourly details** only when you need exact values, then scan the model charts.
6. Scan signal tiles, external context, recent precipitation, observations, and the NWS Area Forecast Discussion.

## Shareable / Embeddable URLs

The dashboard accepts four query parameters. When all four are present and valid, the forecast loads automatically — no need to click **Get Forecast**. Clicking **Get Forecast** also writes the current selections back to the URL so the page can be shared or bookmarked.

| Param  | Value                                  | Example              |
|--------|----------------------------------------|----------------------|
| `m`    | MTNS key (mountain)                    | `hood`               |
| `r`    | Route slug (within that mountain)      | `hogsback`           |
| `start`| Climb start, `YYYY-MM-DDTHH:MM` (local) | `2026-05-14T04:00`  |
| `end`  | Climb end, `YYYY-MM-DDTHH:MM` (local)   | `2026-05-14T16:00`  |

Example:

```
https://rkaika.github.io/rkmountains/mw.html?m=hood&r=hogsback&start=2026-05-14T04:00&end=2026-05-14T16:00
```

Mountain keys: `baker`, `rainier`, `campMuir`, `glacierPeak`, `stHelens`, `adams`, `hood`, `olympus`, `mailbox`, `shuksan`, `shasta`, `denali`. Route slugs are listed in the **Supported Routes Reference** table below.

To run it locally instead:

1. Serve the folder from this repo:

   ```sh
   python3 -m http.server 8766
   ```

2. Visit:

   ```txt
   http://localhost:8766/
   ```

## Interpreting The Output

The Go / Watch / Caution verdict is only a planning aid. It is not a substitute for judgment, current observations, avalanche forecasts, route condition reports, or turning around.

Use the NWS temperatures as the baseline for expected surface conditions. Use the Open-Meteo model comparison to understand uncertainty, especially for wind, freezing level, and precipitation timing. Wide model spread means the plan deserves more caution and another check closer to departure.

## Files

- `index.html`: redirects to `mw.html` (default entry point).
- `mw.html`: current mountaineering weather dashboard.
- `mw3.html`: latest experimental/source copy used before promoting to `mw.html`.
- `mw2.html`: prior dashboard version kept for comparison.
- `mw1.html`: earlier dashboard version kept for comparison.
- `mountain-weather-window.html`: earlier NWS-focused weather-window prototype.

## Planned Improvements

- Customizable Go / Watch / Caution criteria in a settings panel.
- Per-user threshold persistence with `localStorage`.
- Cleaner handling for model availability by forecast horizon.

## Supported Objectives Reference

Thresholds are listed as `W sustained wind go/watch`, `G gust go/watch`, and `P precipitation probability go/watch`.

| Objective | Summit/reference coordinate | Elevation | NWS office | Go/Watch thresholds | Context links |
|---|---:|---:|---|---|---|
| Mt Baker | 48.7767, -121.8144 | 10,781 ft | SEW | W 20/30, G 30/40, P 20/40 | nwac, volcano, webcam |
| Mt Rainier | 46.8529, -121.7604 | 14,411 ft | SEW | W 15/25, G 25/35, P 15/30 | nwac, volcano, nps, webcam |
| Camp Muir | 46.8356, -121.7328 | 10,188 ft | SEW | W 20/30, G 30/40, P 20/40 | nwac, nps, webcam, wta |
| Glacier Peak | 48.1127, -121.1137 | 10,541 ft | SEW | W 20/30, G 30/40, P 20/35 | nwac, volcano |
| Mt St Helens | 46.1912, -122.1944 | 8,366 ft | PQR | W 25/35, G 35/45, P 20/40 | nwac, volcano, nps |
| Mt Adams | 46.2024, -121.4909 | 12,281 ft | PQR | W 20/30, G 30/40, P 20/40 | nwac, volcano, nps |
| Mt Hood | 45.3735, -121.6960 | 11,249 ft | PQR | W 20/30, G 30/40, P 20/40 | nwac, volcano, nps, webcam |
| Mt Olympus | 47.8013, -123.7108 | 7,980 ft | SEW | W 20/30, G 30/40, P 20/35 | nwac, nps |
| Mailbox Peak | 47.4624, -121.6393 | 4,841 ft | SEW | W 25/35, G 35/45, P 20/40 | nwac, wta |
| Mt Shuksan | 48.8275, -121.6149 | 9,131 ft | SEW | W 20/30, G 30/40, P 20/35 | nwac, webcam |
| Mt Shasta | 41.4092, -122.1944 | 14,179 ft | MFR | W 15/25, G 25/35, P 15/30 | avalanche, volcano, nps |
| Mt Denali | 63.0692, -151.0070 | 20,310 ft | AFC | W 15/25, G 25/35, P 15/30 | nps |

## Supported Routes Reference

Route aspect is approximate and is used for wind-exposure hints. Round-trip miles are shown where well-documented; routes without RT data show `—` and the dashboard's crumb header gracefully omits the miles segment.

The **Slug** column is the value to pass as the `r` URL parameter (scoped to the mountain `m`).

| Objective (`m`) | Route/trailhead | Slug (`r`) | Coordinate | Elevation | Route aspect | Miles RT | AllTrails |
|---|---|---|---:|---:|---:|---:|---|
| `baker` | Heliotrope Ridge — Coleman Glacier | `coleman` | 48.8022, -121.8947 | 3,700 ft | 330° | 9 | yes |
| `baker` | Shannon Creek — Easton Glacier | `easton` | 48.7068, -121.8129 | 3,350 ft | 180° | — | yes |
| `baker` | Boulder Ridge | `boulder` | 48.7870, -121.7470 | 4,200 ft | 90° | — | search fallback |
| `rainier` | Paradise — Muir Snowfield / DC route | `dc` | 46.7860, -121.7350 | 5,400 ft | 180° | 16 | yes |
| `rainier` | White River — Emmons Glacier | `emmons` | 46.9020, -121.6427 | 4,250 ft | 45° | 17 | yes |
| `rainier` | Mowich Lake — Tahoma Cleaver | `tahoma` | 46.9335, -121.8638 | 4,929 ft | 270° | — | search fallback |
| `rainier` | Carbon River — Willis Wall / Liberty | `liberty` | 46.9940, -121.9160 | 1,800 ft | 0° | — | search fallback |
| `campMuir` | Paradise — Muir Snowfield | `paradise` | 46.7860, -121.7350 | 5,400 ft | 180° | 9 | yes |
| `glacierPeak` | Suiattle River — Sitkum Glacier | `sitkum` | 48.2520, -121.1810 | 1,850 ft | 315° | — | search fallback |
| `glacierPeak` | N Fork Sauk — White Chuck Glacier | `whitechuck` | 48.1680, -121.1438 | 2,200 ft | 270° | — | search fallback |
| `stHelens` | Marble Mountain Sno-Park — Worm Flows | `wormflows` | 46.1298, -122.1712 | 2,700 ft | 180° | 12 | yes |
| `stHelens` | Climbers Bivouac — Monitor Ridge | `monitor` | 46.1471, -122.1838 | 3,800 ft | 180° | 10 | yes |
| `adams` | Cold Springs — South Climb | `southclimb` | 46.1359, -121.4977 | 5,575 ft | 180° | 12 | yes |
| `adams` | Morrison Creek — SW Chutes | `swchutes` | 46.1760, -121.4540 | 4,600 ft | 225° | — | search fallback |
| `adams` | Killen Creek — North Ridge | `northridge` | 46.2890, -121.5460 | 4,315 ft | 0° | — | search fallback |
| `hood` | Timberline — South Side / Hogsback | `hogsback` | 45.3309, -121.7113 | 5,960 ft | 180° | 8 | yes |
| `hood` | Cloud Cap — Cooper Spur / Sunshine | `cooperspur` | 45.4019, -121.6537 | 5,750 ft | 45° | 7 | search fallback |
| `olympus` | Hoh Rain Forest — Blue Glacier | `hoh` | 47.8608, -123.9343 | 575 ft | 270° | 44 | yes |
| `mailbox` | Mailbox Peak TH — New Trail | `new` | 47.4667, -121.6735 | 900 ft | 315° | 9.4 | yes |
| `mailbox` | Mailbox Peak TH — Old Trail | `old` | 47.4667, -121.6735 | 900 ft | 315° | 5.4 | yes |
| `shuksan` | Artist Point — Price / Sulfide Glacier | `sulfide` | 48.8460, -121.6920 | 5,200 ft | 180° | — | search fallback |
| `shuksan` | Shannon Ridge — NW Couloir | `nwcouloir` | 48.8880, -121.6920 | 3,200 ft | 315° | — | search fallback |
| `shasta` | Bunny Flat — Avalanche Gulch | `avygulch` | 41.3537, -122.2336 | 6,950 ft | 225° | 11 | yes |
| `shasta` | Clear Creek TH | `clearcreek` | 41.3700, -122.1540 | 5,760 ft | 180° | — | search fallback |
| `shasta` | Brewer Creek — Hotlum-Bolam | `hotlum` | 41.4420, -122.0920 | 6,990 ft | 45° | — | search fallback |
| `denali` | Kahiltna Base Camp — West Buttress | `wb` | 62.9667, -151.1500 | 7,200 ft | 180° | — | search fallback |
| `denali` | Wonder Lake — Muldrow Glacier | `muldrow` | 63.4775, -150.8728 | 2,000 ft | 0° | — | search fallback |
