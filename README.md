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
