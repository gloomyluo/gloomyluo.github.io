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
│   └── resorts.html        # 85 Chinese national tourist resorts map
├── docs/                   # Project documentation
└── AGENTS.md               # This file
```

## Tech Stack
- **Frontend**: Pure HTML/CSS/JavaScript (no frameworks)
- **Map**: Leaflet.js with Gaode/AMap tiles
- **Coordinate System**: WGS84 → GCJ02 transformation (China map requirement)
- **Hosting**: GitHub Pages

## Key Features

### Travel Resorts Map (`travel/resorts.html`)
- 85 national-level tourist resorts (国家级旅游度假区)
- 7 batches, last updated June 2024
- Interactive map with region-colored markers
- Search and filter functionality
- Mobile-responsive design (42vh map on mobile, 520px on desktop)
- Table supports horizontal scroll on mobile
- Statistics cards with 2-column grid layout

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

### Update Resort Data
1. Edit `travel/resorts.html`
2. Update the `resorts` array with new data
3. Verify coordinates are in GCJ02 format
4. Test on mobile viewport

### Add New Section
1. Create directory (e.g., `tech/`)
2. Create `index.html` in that directory
3. Add card to main `index.html`
4. Commit: `git add -A && git commit -m "feat: add [section]" && git push`
