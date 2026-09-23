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
├── docs/                   # Project documentation
└── AGENTS.md               # This file
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
