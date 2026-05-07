# Deploying to GitHub Pages

This site is fully static and ships with a graceful fallback for the parts of the
dashboard that normally hit a local Flask backend (`tileserver.py`). Everything
under this folder can be pushed to a GitHub repo and served via Pages without
any server-side runtime.

## TL;DR

```bash
# 1. one-time, in this folder
git init -b main
git add .gitignore .nojekyll
git add .                              # picks up everything else
git commit -m "Initial commit"
git remote add origin git@github.com:<you>/<repo>.git
git push -u origin main

# 2. on github.com:
#    Settings -> Pages -> Source: "Deploy from a branch"
#                       Branch:   main / (root)
```

The site will be live at `https://<you>.github.io/<repo>/`.

## What was set up for GitHub Pages

- `.nojekyll` — disables Jekyll so files starting with `_` are served verbatim.
- `.gitignore` — keeps editor metadata, Python venvs, the 405 MB raw GeoJSON,
  and `martin.zip` out of the repo. The two `.pmtiles` tilesets stay in the
  repo as ordinary files: GitHub Pages does **not** serve Git LFS objects
  through the Pages CDN, so anything the browser needs to fetch must be
  committed directly. The largest committed file (`vacancy_predictions.pmtiles`,
  ~46 MB) sits comfortably under GitHub's 100 MB per-file hard limit.

## What runs in static mode vs. local-server mode

`dashboard.html` auto-detects the host. When loaded from `localhost` /
`127.0.0.1` it tries the local Flask backend first; on any other host it skips
the backend entirely.

| Feature | Local-server mode (tileserver.py) | Static / GitHub Pages mode |
|---|---|---|
| Map basemap & PMTiles | Same — basemap from CARTO, vector parcels from `vacancy_predictions.pmtiles` | Same |
| Parcel popups (click) | Full property bag from PMTiles | Full property bag from PMTiles |
| **SHAP risk drivers** | From `dashboard_shap.json` | From `dashboard_shap.json` |
| Ward choropleth | From `ward_stats.json` + `ward_boundaries.geojson` | Same |
| Sidebar summary cards | From `/summary` endpoint | Aggregated from `ward_stats.json` |
| Ward filter list | From `/wards` endpoint | From `ward_stats.json` |
| Ward fly-to | From `/ward_bounds` endpoint | Computed client-side from the ward boundary GeoJSON |
| Parcel search | DB-wide search via `/search` | Limited to parcels currently rendered in view (`queryRenderedFeatures`) |
| Census tract filter | From `/census_tracts` and `/tract_bounds` | Disabled unless `census_tracts.json` is shipped |

If you want full DB-wide search and tract filtering on Pages, pre-export
`census_tracts.json` (and optionally a small parcel index) from your local
PostGIS instance and commit it next to the HTML.

## Hosting the large files

The two PMTiles tilesets are the heavy pieces:

- `vacancy_predictions.pmtiles` (~46 MB) — full citywide.
- `vacancy_flagged.pmtiles` (~2.2 MB) — top 1 % flagged subset.

Both are tracked via Git LFS by default. If you'd rather host them on S3,
Cloudflare R2, or any static bucket, set the `PMTILES_URL` constant at the top
of the `<script>` block in `dashboard.html` to the absolute URL — the
PMTiles JS reader streams ranges over HTTP.

## Files to keep

The site at minimum needs:

- `dashboard.html`, `Vacancy Risk Landing Page.html`, `PhillyStat360 v2.html`
- `assets/`, `fonts/`, `colors_and_type.css`
- `ward_stats.json`, `ward_boundaries.geojson`, `dashboard_shap.json`
- `vacancy_predictions.pmtiles`, `vacancy_flagged.pmtiles`

`tileserver.py`, `load_db.py`, the raw `*.geojson` exports, and `martin.zip`
are only needed if you're regenerating the data locally — they can be dropped
from a deployment if repo size matters.
