# 交互式WebGIS平台 | Interactive WebGIS Platform

生成自包含轻量级 WebGIS：Leaflet 底图 + 渲染叠加层 + POI 监测点图层 + **点击即查**（内嵌降采样栅格 JSON，浏览器端最近邻查询高程）+ 图层开关面板。无需后端。

属性查询引擎支持 gt/lt/ge/le/eq/contains 六种运算符，可单测；另把点要素聚合成密度栅格。

## 核心算法

query_value_at 双线性点查询 + nearest_query 最近邻 → build_layer_config 图层配置 → point_density_raster 聚合 → Leaflet+内嵌 GRID 组装。

## 依赖

```bash
pip install numpy rasterio scipy matplotlib geopandas shapely pillow
```

## 使用方法

### 示例 1（合成数据，离线）

```bash
python geoskill-interactive-webgis.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### 示例 2（属性查询）

```bash
python geoskill-interactive-webgis.py --input poi.geojson --query-field value --query-op gt --query-value 50
```

### 示例 3（contains 查询）

```bash
python geoskill-interactive-webgis.py --input poi.geojson --query-field category --query-op contains --query-value school
```

### 示例 4（合成 200 个 POI）

```bash
python geoskill-interactive-webgis.py --bbox 116 39 117 40 --synthetic --n-points 200
```

### 示例 5（自定义颜色与标题）

```bash
python geoskill-interactive-webgis.py --bbox 116 39 117 40 --synthetic --color "#e6550d" --title "城市设施"
```

## 输出

| 文件 | 格式 | 说明 |
|---|---|---|
| `webgis.html` | HTML | WebGIS 应用（主产物） |
| `webgis_data.json` | JSON | 栅格网格/站点/配置（可验证产物） |
| `features.geojson` | GeoJSON | 点要素 |
| `density.tif` | GeoTIFF | 点密度栅格 |

每次运行还会产出 `output-manifest.json`（运行清单）。

## 数据源 / Source

本地 GeoTIFF / 矢量文件；`--synthetic` 模式生成物理一致的模拟数据，完全离线。

## 隐私声明 / Privacy

- 默认离线运行，`--synthetic` 模式完全无网络。
- 所有处理在本地完成，不上传用户数据。

## License

MIT
