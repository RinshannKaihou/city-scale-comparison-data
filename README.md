# city-scale-comparison-data

Stitched OpenStreetMap road network data for the [city-scale-comparison](https://github.com/RinshannKaihou/city-scale-comparison) app.

This repo is a **data-only mirror** so the app repo can stay small (~10 MB instead of ~820 MB). The app fetches per-city files at runtime via [jsDelivr](https://www.jsdelivr.com/):

```
https://cdn.jsdelivr.net/gh/RinshannKaihou/city-scale-comparison-data@main/<city-id>.json
```

## Contents

79 files, one per city. Each file is a JSON array of polylines, where each polyline is an array of `[lng, lat]` pairs:

```json
[[[lng, lat], [lng, lat], ...], [[lng, lat], ...], ...]
```

Total uncompressed size: ~251 MB. Largest single file: `tokyo.json` at ~28 MB.

## How this is generated

Files are produced by the pipeline in the [main app repo](https://github.com/RinshannKaihou/city-scale-comparison):

1. `scripts/fetch-roads-overpass.js` — bbox-scoped Overpass queries against OSM
2. `scripts/stitch-roads.js` — angle-based merge of way fragments into continuous polylines

See [CLAUDE.md](https://github.com/RinshannKaihou/city-scale-comparison/blob/main/CLAUDE.md) in the app repo for the gotchas.

## Versioning

Tagged snapshots:
- `data-v1` — initial release, 2026-05-23, 79 cities.

The app's default fetch URL uses `@main` for "latest." Pin to a tag via `@data-v1` if you need stability.

## License

© [OpenStreetMap contributors](https://www.openstreetmap.org/copyright), [Open Data Commons Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/).
