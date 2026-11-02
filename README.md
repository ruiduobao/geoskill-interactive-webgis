# Interactive WebGIS Platform (geoskill-interactive-webgis)

> Configure a lightweight WebGIS with query support as a self-contained HTML app

---

## 1. Overview

Generates a self-contained lightweight WebGIS: Leaflet base map + rendered overlay layers + POI monitoring-point layer + **click-to-query** (embedded downsampled raster JSON with browser-side nearest-neighbor elevation lookup) + a layer toggle panel. No backend required. The attribute query engine supports six operators — gt/lt/ge/le/eq/contains — and is unit-testable; point features are also aggregated into a density raster.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-interactive-webgis.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `webgis.html` | HTML | WebGIS application (primary output) |
| `webgis_data.json` | JSON | Raster grid/sites/config (verifiable output) |
| `features.geojson` | GeoJSON | Point features |
| `density.tif` | GeoTIFF | Point density raster |

Each run also produces `output-manifest.json` (run manifest).

## 6. Technical Principle

query_value_at bilinear point query + nearest_query nearest neighbor → build_layer_config layer configuration → point_density_raster aggregation → Leaflet + embedded GRID assembly.

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
