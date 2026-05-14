# RK Mountains

Small static mountaineering weather tools for comparing climb windows on Cascade and west-coast volcano routes.

## Main Page

Open `index.html` or `mountain-weather.html` to use the unified mountain weather dashboard. `index.html` is the default entry point and currently mirrors `mountain-weather.html`.

The page helps evaluate a selected mountain, trailhead/route, and climb window. It combines official NWS point forecasts with raw model guidance so you can compare the human-edited baseline against multiple numerical models.

## What Is On The Page

- **Mountain and route controls**: choose a peak, trailhead/route, climb start, and climb end.
- **Go / Watch / Stop verdict**: a quick decision aid based on wind, gust, and precipitation thresholds for the selected mountain.
- **Summary cards**: summit temperature, trailhead temperature, peak wind, peak gust, freezing level, precipitation probability, snow signal, and model spread.
- **Hourly table**: hour-by-hour summit and trailhead temperatures alongside wind, gust, direction, freezing level, precipitation probability, sky cover, and notes.
- **Model charts**: Open-Meteo model comparison charts for wind, gusts, freezing level, and precipitation probability.
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

1. Open `index.html` in a browser, or serve the folder locally:

   ```sh
   python3 -m http.server 8766
   ```

2. Visit:

   ```txt
   http://localhost:8766/
   ```

3. Select a mountain and route/trailhead.
4. Set your climb start and expected end time.
5. Click **Get Forecast**.
6. Read the NWS summit/trailhead temperatures first, then compare model spread, wind/gust charts, freezing level, precipitation, and the NWS discussion.

## Interpreting The Output

The Go / Watch / Stop verdict is only a planning aid. It is not a substitute for judgment, current observations, avalanche forecasts, route condition reports, or turning around.

Use the NWS temperatures as the baseline for expected surface conditions. Use the Open-Meteo model comparison to understand uncertainty, especially for wind, freezing level, and precipitation timing. Wide model spread means the plan deserves more caution and another check closer to departure.

## Files

- `index.html`: default app entry point.
- `mountain-weather.html`: unified mountain weather dashboard.
- `summit_weather.html`: earlier Open-Meteo-focused summit dashboard.
- `mountain-weather-window.html`: earlier NWS-focused weather-window prototype.

## Planned Improvements

- Customizable Go / Watch / Stop criteria in a settings panel.
- Per-user threshold persistence with `localStorage`.
- Cleaner handling for model availability by forecast horizon.
