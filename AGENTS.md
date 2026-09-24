# Blog Project Guide

## Project Overview
- **Repository**: gloomyluo/gloomyluo.github.io
- **URL**: https://gloomyluo.github.io
- **Local Path**: E:\AIAgentProject\blog
- **Git User**: gloomyluo
- **Git Email**: gloomyluo@users.noreply.github.com

## Directory Structure
```
blog/
├── index.html              # Blog homepage with navigation cards
├── travel/
│   ├── index.html          # Enhanced travel map (split view + drawer + holiday heat)
│   ├── resorts.html        # Legacy resorts-only map (85 national resorts)
│   ├── img/                # Local images for list cards (att_/fam_/res_*.jpg)
│   └── data/
│       ├── resorts.json    # 86 national tourist resorts
│       ├── attractions.json # 153 attractions (125×5A + 28×4A)
│       ├── hotels.json     # 63 family hotels/theme parks
│       └── regions.json    # 7 regions with feature tags
├── hotel/
│   └── index.html          # 国庆酒店库存地图 (5369 hotels, 7 groups, 149 brands)
├── docs/                   # Project documentation
└── AGENTS.md               # This guide
```

## Tech Stack
- **Frontend**: Pure HTML/CSS/JavaScript (no frameworks)
- **Map**: Leaflet.js with Gaode/AMap tiles
- **Coordinate System**: WGS84 → GCJ02 transformation (China map requirement)
- **Hosting**: GitHub Pages

## Key Features

### Travel Map (`travel/index.html`) - Enhanced Version
- 302 total items: 86 resorts + 153 attractions + 63 family hotels/parks
- **Split View**: Airbnb-style list (420px) + sticky map (no fullscreen modal)
- **Detail**: Map leaflet popup + left-panel drawer (full info)
- **Holiday Heat**: Toolbar holiday picker (public-holidays API) × local heat → leaflet.heat layer
- **Grades**: 5A/4A badges on cards, popups, and drawer
- **Local Images**: Bing-matched scenery photos stored in `travel/img/`
- **Region Features**: 7 regions with cultural/cuisine tags
- **Data Split**: JSON files in `travel/data/` for easy maintenance
- Mobile-responsive (stacked layout ≤900px)

### Legacy Resorts Map (`travel/resorts.html`)
- 85 national-level tourist resorts only
- Original single-file implementation

### Hotel Inventory Map (`hotel/index.html`)
- **Source Project**: `E:\AIAgentProject\Daily\hotel_inventory` (build via `build_map.py`)
- **Data**: 5369 hotels, 7 groups (万豪/洲际/希尔顿/凯悦/雅高/温德姆/华住), 149 brands, 57 cities
- **Tags**: 高端 1809 · 商务 1984 · 城市 927 · 度假 641 · 亲子 8
- **Prices**: 飞猪房价 3752/5369 (69.9%), unit ¥/night, check-in 2026-10-02
- **Features**:
  - 高德底图 + Leaflet markercluster (5369 points)
  - 类型/集团/城市/品牌/星级多维筛选 + 关键词搜索
  - 侧边栏列表（前 400 条）+ 城市名点击定位
  - 缩放至 zoom≥16 视口内所有 marker 自动展开弹窗（autoClose:false）
  - 弹窗含价格、评分、标签、携程详情链接、去哪儿 App 预订跳转
- **Map Configuration**: Same as travel map (Gaode tiles, GCJ02 coords)
- **Update Flow**: 修改 `hotel_inventory/build_map.py` → `python build_map.py` → 复制 `output/hotel_map.html` 到 `blog/hotel/index.html` → commit & push

### Map Configuration
- **Tile Provider**: Gaode/AMap (not OpenStreetMap, which fails in China)
- **Tile URL**: `https://webrd0{s}.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=8&x={x}&y={y}&z={z}`
- **CRS**: EPSG3857 (standard web mercator)
- **Coordinate Fix**: All markers use GCJ02 coordinates (offset ~500m from WGS84)

## Git Configuration
- **Proxy**: Direct connection works (no proxy needed)
- **Credentials**: Project-scoped at `.git/.git-credentials`
- **Branch**: master

## Development Notes

### Adding New Pages
1. Create HTML file in appropriate subdirectory (e.g., `travel/`, `tech/`, `life/`)
2. Follow existing HTML structure and styling conventions
3. Update `index.html` to add navigation card for new section
4. Commit and push

### Mobile Optimization Checklist
- Map height: `42vh` (mobile) / `520px` (desktop)
- Filter buttons: horizontal scroll, no wrap
- Table: horizontal scroll with visual hint
- Touch feedback: `:active` scale effect
- Font sizes: responsive with media queries

### Data Sources
- Tourist resorts data compiled from official government announcements
- Coordinates verified against Gaode Maps
- Last verified: September 2026

## Security Notes
- Never commit credentials or tokens to git
- `.gitignore` excludes `*.credentials` and `.git-credentials`
- GitHub Push Protection is enabled - will reject pushes containing secrets

## Common Tasks

### Update Travel Map Data
1. Edit JSON files in `travel/data/`:
   - `resorts.json` - National tourist resorts
   - `attractions.json` - Curated 5A attractions
   - `hotels.json` - Family hotels and theme parks
   - `regions.json` - Region colors and feature tags
2. Coordinates must be in WGS84 (auto-converted to GCJ02)
3. Test on mobile viewport

### Add New Section
1. Create directory (e.g., `tech/`)
2. Create `index.html` in that directory
3. Add card to main `index.html`
4. Commit: `git add -A && git commit -m "feat: add [section]" && git push`

### Update Hotel Inventory Map
1. Source project at `E:\AIAgentProject\Daily\hotel_inventory`
2. Edit `build_map.py` (map config/JS logic) or data scripts (prices/coords/tags)
3. Regenerate: `python build_map.py` → `output/hotel_map.html`
4. Deploy: copy to `blog/hotel/index.html` → commit & push
5. Key files in source project:
   - `build_map.py` — map generator (HTML/JS/CSS all inline)
   - `fetch_prices.py` / `fetch_prices2.py` — 飞猪房价抓取
   - `scrape_brands.py` — 携程品牌页库存抓取
   - `enrich_coords4.py` — 坐标补全
   - `tag_types.py` — 类型标签
   - `output/hotels_raw.json` — 主数据（5369 家，含坐标/标签/价格）
   - `output/coords.json` — 坐标库
   - `PROGRESS.md` — 项目进展文档
