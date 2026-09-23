# Development Log

## 2026-09-22: Initial Setup

### Tasks Completed
1. **Data Compilation**
   - Researched and compiled list of 85 national-level tourist resorts (国家级旅游度假区)
   - Data spans 7 batches, last updated June 2024
   - Included: name, province, region, description, batch number, GPS coordinates

2. **Excel Export**
   - Created `国家级旅游度假区名录.xlsx` with multi-level hierarchy
   - Path: E:\AIAgentProject\Daily\国家级旅游度假区名录.xlsx

3. **Interactive Map Page**
   - Built `travel/resorts.html` (27KB)
   - Features: Leaflet map, Gaode tiles, GCJ02 coordinates, search, filter, responsive table
   - Mobile-optimized: 42vh map, horizontal scroll table, touch feedback

4. **Blog Structure**
   - Created `index.html` homepage with card navigation
   - Directory structure: `travel/` subdirectory

5. **GitHub Pages Deployment**
   - Repository: gloomyluo/gloomyluo.github.io
   - Pushed to master branch
   - Removed credentials from git history using filter-branch

6. **Project Migration**
   - Moved from `E:\AIAgentProject\Daily\gloomyluo.github.io` to `E:\AIAgentProject\blog`
   - Configured project-scoped git credentials

### Technical Challenges Solved
- **OpenStreetMap blocked in China**: Switched to Gaode/AMap tiles
- **Coordinate offset**: Implemented WGS84 → GCJ02 transformation
- **Git push rejected (GitHub Push Protection)**: Cleaned credentials from history
- **Proxy issues**: FlClash on port 47890, but direct connection works

### Files Created
- `index.html` - Blog homepage
- `travel/resorts.html` - Tourist resorts interactive map
- `AGENTS.md` - Project guide for AI agents
- `docs/development-log.md` - This file
- `.gitignore` - Excludes credentials and system files

### GitHub URLs
- Homepage: https://gloomyluo.github.io
- Travel Map: https://gloomyluo.github.io/travel/resorts.html

---

## 2026-09-23: Travel Map Enhancement

### Tasks Completed
1. **Data Expansion**
   - Added 50 curated 5A attractions (`attractions.json`)
   - Added 20 family hotels/theme parks (`hotels.json`)
   - Added region features for 7 regions (`regions.json`)
   - Total: 155 items across 3 categories

2. **Architecture Refactor**
   - Split data into separate JSON files
   - New unified page `travel/index.html`
   - Kept legacy `resorts.html` for backward compatibility

3. **New Features**
   - **Layer Control**: Independent toggle for resorts/attractions/hotels
   - **Cascade Menu**: Region navigation → feature tags → item list
   - **Heatmap**: Optional density visualization (leaflet.heat)
   - **Region Features**: Cultural/cuisine tags per region
   - **Type Filters**: Filter table by category

4. **Security**
   - Updated `.gitignore` to exclude `*credential*`
   - Removed accidentally staged credentials file

### Files Created/Modified
- `travel/index.html` - New enhanced map (542 lines)
- `travel/data/resorts.json` - 85 resorts
- `travel/data/attractions.json` - 50 attractions
- `travel/data/hotels.json` - 20 hotels/parks
- `travel/data/regions.json` - 7 regions with features
- `index.html` - Updated navigation card
- `.gitignore` - Added credential patterns
- `AGENTS.md` - Updated documentation

### GitHub URLs
- Homepage: https://gloomyluo.github.io
- Enhanced Map: https://gloomyluo.github.io/travel/index.html
- Legacy Map: https://gloomyluo.github.io/travel/resorts.html

---

## 2026-09-23: Split View, Holiday Heat, Data Expansion

### Tasks Completed
1. **UI Rework (user feedback driven)**
   - Removed Hero "发现中国之美" and 热门推荐 sections
   - Airbnb-style split layout: left 420px scrolling list + sticky map
   - Replaced fullscreen modal with map popup + list-column drawer
   - Full-viewport fixed layout (`body overflow hidden`, max-width 1600px)

2. **Holiday Heat Toolbar**
   - Public holiday API: `https://public-holidays.toolhub.run/api/public-holidays?year=YYYY&code=cn`
   - View toggle: `标记点` / `🔥 节假日热力` (leaflet.heat)
   - Heat = local attraction heat × holiday coefficient (春节1.6/国庆1.5/五一1.4/…)
   - Noted in UI: real-time crowd APIs need enterprise keys

3. **Data Expansion + Local Images**
   - Attractions: 60 → **153** (125×5A + 28×4A)
   - Family: 20 → **63**
   - Resorts: 86 (re-imaged, fixed `price:"free"` → `免费`)
   - Images: Bing image search → download → 480×360 JPEG in `travel/img/` (302 files)
   - Abandoned picsum/placehold (not scenic); Wikipedia/Baidu/DuckDuckGo blocked
   - Grade badges (5A red / 4A orange) on cards, popup, drawer

### Files Modified
- `travel/index.html` - Split view, drawer, holiday heat, grade badges
- `travel/data/attractions.json` - 153 attractions with `g`/`img`/`heat`
- `travel/data/hotels.json` - 63 family items with local images
- `travel/data/resorts.json` - 86 resorts, local images, price fix
- `travel/img/` - 302 local JPEGs (att_/fam_/res_*.jpg)
- `AGENTS.md` - Updated structure and feature docs

### GitHub URLs
- Homepage: https://gloomyluo.github.io
- Enhanced Map: https://gloomyluo.github.io/travel/index.html
- Legacy Map: https://gloomyluo.github.io/travel/resorts.html

---

## Future Tasks
- [ ] Add more sections (tech blog, life notes, etc.)
- [ ] Implement dark mode toggle
- [ ] Add holiday recommendation labels
- [ ] Add distance measurement tool
- [ ] Add route planner for multi-stop trips
- [ ] Optimize page load speed
- [ ] Add analytics (optional)
- [ ] Add Ctrip deep links for new attractions/family items
