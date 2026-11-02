---
name: geoskill-interactive-webgis
description: 'Configure a lightweight WebGIS with query support as a self-contained HTML app'
---

# 交互式WebGIS平台 | Interactive WebGIS Platform

Generates a self-contained lightweight WebGIS: Leaflet base map + rendered overlay layers + POI monitoring point layer + **click-to-query** (embedded downsampled raster JSON, browser-side nearest-neighbor elevation query) + layer toggle panel. No backend required.

The attribute query engine supports six operators — gt/lt/ge/le/eq/contains — and is unit-testable; it also aggregates point features into a density raster.

## Core Algorithm / 核心算法

query_value_at bilinear point query + nearest_query nearest-neighbor → build_layer_config layer configuration → point_density_raster aggregation → Leaflet + embedded GRID assembly.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy matplotlib geopandas shapely pillow
```

## Usage / 使用方法

### Example 1 (synthetic data, offline)

```bash
python geoskill-interactive-webgis.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2 (attribute query)

```bash
python geoskill-interactive-webgis.py --input poi.geojson --query-field value --query-op gt --query-value 50
```

### Example 3 (contains query)

```bash
python geoskill-interactive-webgis.py --input poi.geojson --query-field category --query-op contains --query-value school
```

### Example 4 (synthetic 200 POIs)

```bash
python geoskill-interactive-webgis.py --bbox 116 39 117 40 --synthetic --n-points 200
```

### Example 5 (custom color and title)

```bash
python geoskill-interactive-webgis.py --bbox 116 39 117 40 --synthetic --color "#e6550d" --title "urban facilities"
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `webgis.html` | HTML | WebGIS application (primary output) |
| `webgis_data.json` | JSON | Raster grid/sites/config (verifiable output) |
| `features.geojson` | GeoJSON | Point features |
| `density.tif` | GeoTIFF | Point density raster |

Each run also produces `output-manifest.json` (run manifest).

## Data Source / 数据源 / Source

Local GeoTIFF / vector files; `--synthetic` mode generates physically consistent simulated data, fully offline.

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is done locally; no user data is uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
