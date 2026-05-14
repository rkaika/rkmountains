# RK Mountains

Small static mountaineering weather tools for comparing climb windows on Cascade and west-coast volcano routes.

## Main Page

Open `mw2.html` (or just `index.html`, which redirects there) to use the mountaineering-focused mountain weather dashboard. Open `mw1.html` for the original version.

The page helps evaluate a selected mountain, trailhead/route, and climb window. It combines official NWS point forecasts with raw model guidance so you can compare the human-edited baseline against multiple numerical models.

## What Is On The Page

- **Mountain and route controls**: choose a peak, trailhead/route, climb start, and climb end.
- **Go / Watch / Caution verdict**: a quick decision aid based on wind, gust, and precipitation thresholds for the selected mountain.
- **Summary cards**: summit temperature, trailhead temperature, peak wind, peak gust, freezing level, precipitation probability, snow signal, and model spread.
- **Hourly table**: hour-by-hour summit and trailhead temperatures alongside wind, gust, direction, freezing level, precipitation probability, sky cover, and notes.
- **Model charts**: Open-Meteo model comparison charts for wind, gusts, freezing level, and precipitation probability.
- **Model guidance for this window**: lead-time-aware advice on which models to lean on (Nowcast / HRRR lead ≤48 h / NAM bridge ≤84 h / Global pattern beyond), updating based on the selected climb start.
- **Interpretation notes**: how to read the NWS baseline, when HRRR leads, how to cross-check globals against mesoscale, and what Model Spread means for confidence.
- **NWS Area Forecast Discussion**: the latest AFD for the relevant forecast office.
- **Dark/light mode**: toggle in the header; the preference is saved in the browser.

## Data Sources

- **Summit and trailhead temperatures**: NWS hourly point forecasts from `api.weather.gov`.
- **Snow signal**: NWS grid forecast data, including snowfall amount where available.
- **Wind, gusts, freezing level, precipitation, and cloud cover**: Open-Meteo model data.
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

Use the hosted GitHub Pages version:

- [Latest dashboard](https://rkaika.github.io/rkmountains/)
- [Mountaineering-focused dashboard](https://rkaika.github.io/rkmountains/mw2.html)
- [Original dashboard](https://rkaika.github.io/rkmountains/mw1.html)

Then:

1. Select a mountain and route/trailhead.
2. Set your climb start and expected end time.
3. Click **Get Forecast**.
4. Read the NWS summit/trailhead temperatures first, then compare the route advisor, critical criteria, phase timeline, model spread, wind/gust charts, freezing level, precipitation, observations, and NWS discussion.

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

- `index.html`: redirects to `mw2.html` (default entry point).
- `mw1.html`: original unified mountain weather dashboard.
- `mw2.html`: mountaineering-focused dashboard.
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

Phase split is the route-weighted planning split used by `mw2.html`: approach / climb / summit block / descent. Route aspect is approximate and is used only for wind-exposure hints.

| Objective | Route/trailhead | Coordinate | Elevation | Route aspect | Phase split | AllTrails |
|---|---|---:|---:|---:|---|---|
| Mt Baker | Heliotrope Ridge — Coleman Glacier | 48.8022, -121.8947 | 3,700 ft | 330° | 20%/45%/10%/25% | yes |
| Mt Baker | Shannon Creek — Easton Glacier | 48.7068, -121.8129 | 3,350 ft | 180° | 20%/45%/10%/25% | yes |
| Mt Baker | Boulder Ridge | 48.7870, -121.7470 | 4,200 ft | 90° | 18%/46%/10%/26% | search fallback |
| Mt Rainier | Paradise — Muir Snowfield / DC route | 46.7860, -121.7350 | 5,400 ft | 180° | 25%/40%/10%/25% | yes |
| Mt Rainier | White River — Emmons Glacier | 46.9020, -121.6427 | 4,250 ft | 45° | 20%/45%/10%/25% | yes |
| Mt Rainier | Mowich Lake — Tahoma Cleaver | 46.9335, -121.8638 | 4,929 ft | 270° | 25%/42%/8%/25% | search fallback |
| Mt Rainier | Carbon River — Willis Wall / Liberty | 46.9940, -121.9160 | 1,800 ft | 0° | 25%/45%/8%/22% | search fallback |
| Camp Muir | Paradise — Muir Snowfield | 46.7860, -121.7350 | 5,400 ft | 180° | 14%/56%/6%/24% | yes |
| Glacier Peak | Suiattle River — Sitkum Glacier | 48.2520, -121.1810 | 1,850 ft | 315° | 35%/38%/7%/20% | search fallback |
| Glacier Peak | N Fork Sauk — White Chuck Glacier | 48.1680, -121.1438 | 2,200 ft | 270° | 35%/38%/7%/20% | search fallback |
| Mt St Helens | Marble Mountain Sno-Park — Worm Flows | 46.1298, -122.1712 | 2,700 ft | 180° | 22%/42%/8%/28% | yes |
| Mt St Helens | Climbers Bivouac — Monitor Ridge | 46.1471, -122.1838 | 3,800 ft | 180° | 18%/44%/8%/30% | yes |
| Mt Adams | Cold Springs — South Climb | 46.1359, -121.4977 | 5,575 ft | 180° | 18%/45%/8%/29% | yes |
| Mt Adams | Morrison Creek — SW Chutes | 46.1760, -121.4540 | 4,600 ft | 225° | 18%/44%/8%/30% | search fallback |
| Mt Adams | Killen Creek — North Ridge | 46.2890, -121.5460 | 4,315 ft | 0° | 22%/45%/8%/25% | search fallback |
| Mt Hood | Timberline — South Side / Hogsback | 45.3309, -121.7113 | 5,960 ft | 180° | 12%/50%/8%/30% | yes |
| Mt Hood | Cloud Cap — Cooper Spur / Sunshine | 45.4019, -121.6537 | 5,750 ft | 45° | 18%/48%/8%/26% | search fallback |
| Mt Olympus | Hoh Rain Forest — Blue Glacier | 47.8608, -123.9343 | 575 ft | 270° | 45%/30%/5%/20% | yes |
| Mailbox Peak | Mailbox Peak TH — New Trail | 47.4667, -121.6735 | 900 ft | 315° | 12%/50%/8%/30% | yes |
| Mailbox Peak | Mailbox Peak TH — Old Trail | 47.4667, -121.6735 | 900 ft | 315° | 8%/56%/6%/30% | yes |
| Mt Shuksan | Artist Point — Price / Sulfide Glacier | 48.8460, -121.6920 | 5,200 ft | 180° | 18%/45%/8%/29% | search fallback |
| Mt Shuksan | Shannon Ridge — NW Couloir | 48.8880, -121.6920 | 3,200 ft | 315° | 22%/45%/8%/25% | search fallback |
| Mt Shasta | Bunny Flat — Avalanche Gulch | 41.3537, -122.2336 | 6,950 ft | 225° | 18%/45%/8%/29% | yes |
| Mt Shasta | Clear Creek TH | 41.3700, -122.1540 | 5,760 ft | 180° | 20%/44%/8%/28% | search fallback |
| Mt Shasta | Brewer Creek — Hotlum-Bolam | 41.4420, -122.0920 | 6,990 ft | 45° | 18%/45%/8%/29% | search fallback |
| Mt Denali | Kahiltna Base Camp — West Buttress | 62.9667, -151.1500 | 7,200 ft | 180° | 15%/60%/10%/15% | search fallback |
| Mt Denali | Wonder Lake — Muldrow Glacier | 63.4775, -150.8728 | 2,000 ft | 0° | 40%/40%/8%/12% | search fallback |
