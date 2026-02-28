---
name: market-research
description: >
  Real estate market research skill for producing comprehensive, data-driven neighborhood and school analysis reports.
  Creates interactive HTML reports with charts (Chart.js), maps (Leaflet.js), and data tables from web-sourced research.
  Use this skill whenever the user asks to research a neighborhood, city, area, or real estate market — including
  school rankings, housing prices, neighborhood comparisons, school-to-price correlation, or community profiles.
  Also trigger when the user mentions "market research", "neighborhood analysis", "school ratings", "property analysis",
  "area report", "housing report", or wants to compare neighborhoods or schools in any geography.
  Even if the user just names a city and says "research it" or "tell me about schools there", use this skill.
---

# Real Estate Market Research

This skill produces comprehensive, interactive HTML research reports analyzing the relationship between school performance, housing prices, and neighborhood characteristics for any geographic area. Reports are built from 40+ web sources, cross-referenced for accuracy, and presented in a polished editorial design system with interactive charts, maps, and data tables.

## What This Skill Produces

The final deliverable is a **single self-contained HTML file** containing:

- A newspaper-style editorial layout with sections, navigation, and a scrolling data ticker
- A stat grid summarizing key figures (population, neighborhoods, schools, price range, etc.)
- An interactive Leaflet.js map with color-coded markers by price tier
- Chart.js visualizations: horizontal bar charts (prices, school ratings), doughnut charts (tier distribution, housing types), scatter/bubble plots (price vs. school rating correlation), vertical bar charts, and line charts
- Filterable neighborhood profile cards with tags, descriptions, and metadata
- School comparison tables with ratings, programs, and rankings
- A correlation analysis section with CSS-rendered premium bars
- A neighborhood segmentation/clustering section
- A methodology section citing all sources
- A source appendix

The report is analytical in tone — it presents data and findings, not marketing copy. Think "research journal" not "real estate brochure."

---

## Workflow Overview

The process has three phases, each building on the last. Don't skip phases or combine them — the quality of the final report depends on the intermediate markdown documents being thorough.

### Phase 1: Research & Data Collection (Markdown Documents)

### Phase 2: Report Synthesis (Interactive HTML)

### Phase 3: Review & Refinement

---

## Phase 1: Research & Data Collection

The goal is to produce **two comprehensive markdown reference documents** — one for neighborhoods, one for schools — sourced from 40+ independent websites. These become the data backbone of the HTML report.

### Tavily Research Best Practices

The quality of the final report depends entirely on the quality of the research inputs. Follow these principles for every Tavily query:

**Query design matters.** Each query should have a clear goal with specific details and direction — not a vague keyword dump. Include the geographic scope, time frame, and what kind of data you're looking for. The more context you provide, the better Tavily's agents can target relevant sources.

**Choose the right model for the job:**
- Use `model: "pro"` for broad, multi-faceted queries that span multiple subtopics (e.g., "competitive landscape of neighborhoods"). Pro deploys multiple sub-agents that explore in parallel — it's slower but dramatically more thorough.
- Use `model: "mini"` for narrow, well-scoped questions where you need one specific data point (e.g., "what is the Fraser Institute rating for Iroquois Ridge HS in 2025"). Mini is faster and more focused.
- Default to `"pro"` for the initial research sweeps, then use `"mini"` for targeted follow-up queries to fill data gaps.

**Share what you already know.** If earlier queries have already established baseline facts (e.g., you know the school boards, the major neighborhoods, approximate price ranges), include that context in subsequent queries. This prevents Tavily from re-discovering things you already have and pushes it toward new information.

**Keep queries clean and directed.** Use a clear task statement + essential context + desired output. Avoid dumping raw background text into the query.

**Example of a strong query:**
```
"Research residential real estate pricing in Oakville, Ontario for Q4 2025 through Q1 2026.
We know Oakville is served by the Halton District School Board and Halton Catholic DSB.
Focus on median listing prices by neighborhood (Old Oakville, Bronte, Joshua Creek, Glen Abbey,
River Oaks, College Park, Clearview, Eastlake, West Oak Trails, Falgarwood).
Include detached, townhouse, and condo segments separately where data is available.
Cite specific listing platforms (zolo.ca, wahi.com, realtor.ca, housesigma.com)."
```

**Example of a weak query:**
```
"Oakville neighborhoods prices 2025 2026 housing"
```

The strong query gives Tavily direction on neighborhoods to look for, price segments to separate, time window, and preferred source types. The weak query returns generic results that require heavy manual filtering.

### Step 1: Neighborhood Research

Run **at least 8 Tavily research queries** covering different angles of the target area. The key is breadth — you want data from real estate platforms, municipal sites, community guides, census data, and local blogs. Don't rely on a single source for any claim.

**Query strategy — start broad, then fill gaps:**

**Round 1 (4 queries, all `model: "pro"`, run in parallel):** These are your foundation queries. Each one explores a broad facet of the area.

1. **Market overview** — `"Comprehensive guide to [City] neighborhoods and residential areas in [current year]. Include all major neighborhoods/communities with approximate home price ranges by housing type (detached, townhouse, condo). We need specific price data, not just 'affordable' or 'expensive'. Cite real estate listing platforms."`

2. **Community profiles** — `"Detailed community profiles for [City], [Province/State] neighborhoods. For each area, cover demographics, cultural makeup, lifestyle amenities (named shopping centers, restaurants, parks), and the general character or vibe of the community. Include municipal and community guide sources."`

3. **Transit & infrastructure** — `"Transit accessibility and transportation infrastructure in [City]. Cover commuter rail stations (e.g., GO Transit), bus routes, highway access, and commute times to major employment centers. Include any planned transit expansions or new developments."`

4. **School-price relationship** — `"How do school quality and school boundary zones affect home prices in [City]? Include data on price premiums in top school catchment areas, specific school names and their impact on nearby property values, and any studies or agent analyses quantifying the school-price correlation."`

**Round 2 (4+ queries, `model: "pro"` or `"mini"`, run after reviewing Round 1 results):** These fill specific gaps identified in Round 1.

- If missing luxury/estate data: `"Luxury homes and estate neighborhoods in [City]. Focus on areas with median prices above $[X]M, lot sizes, prestige factors, and what drives the premium pricing."`
- If missing new developments: `"New master-planned communities and developments in [City] [current year]. Include builder names, project phases, expected price ranges, and planned amenities."`
- If specific neighborhoods lack detail: `"Detailed profile of [Neighborhood], [City] including current home prices, schools, parks, demographics, and notable amenities. We already know it's in the [price range] range but need specifics on [gap]."`
- If cultural/diversity data is thin: `"Cultural diversity and multicultural communities in [City]. Which neighborhoods have significant [specific community] populations? Include cultural venues, religious institutions, and ethnic commercial areas."`

Use `model: "mini"` for Round 2 queries that target a single neighborhood or data point. Use `model: "pro"` for queries that still span multiple topics.

**Compile into `[area]-neighborhoods.md`** with this structure for each neighborhood:

```markdown
### [Neighborhood Name]

#### Overview
[2-3 sentences on character and positioning]

#### Location & Boundaries
[Geographic context, major roads, relative position]

#### Housing Types & Prices
[Specific price ranges by housing type, sourced from listing data]

#### Demographics
[Cultural makeup, family composition, socioeconomic profile]

#### Amenities & Lifestyle
[Notable commercial areas, restaurants, malls, cultural venues]

#### Parks & Recreation
[Named parks, trails, recreation centers]

#### Transit & Transportation
[GO stations, bus routes, highway access, commute times]

#### Schools
[Key schools serving the area with ratings if available]

#### Character/Vibe
[What makes this neighborhood distinctive]
```

Every neighborhood should have **specific price ranges** (not vague "affordable" or "expensive"), **named schools** with ratings where available, and **named amenities** (actual park names, mall names, etc.).

### Step 2: School Research

Run **at least 6 Tavily research queries** focused on education, using the same query design principles.

**Round 1 (3 queries, `model: "pro"`, run in parallel):**

1. **Rankings overview** — `"Complete school rankings for [City], [Province/State] in [current year]. Include both elementary and secondary schools. We need Fraser Institute ratings (or equivalent standardized rating system), EQAO scores, and Ontario/provincial rankings. Cover both public ([board name]) and Catholic ([board name]) schools. Provide the actual numerical ratings, not just 'top-rated'."`

2. **Programs & specializations** — `"Specialized academic programs available in [City] schools including French Immersion, International Baccalaureate (IB), Advanced Placement (AP), Gifted programs, STEM/STREAM, arts programs, and High Performance Athletics. Which schools offer which programs? Include both elementary and secondary levels."`

3. **Private & independent schools** — `"Private and independent schools in [City] and surrounding area. Include school names, grade levels served, tuition ranges, notable programs, religious affiliation if any, and any ranking data available. Cover both day schools and boarding options."`

**Round 2 (3+ queries, `model: "mini"`, run after reviewing Round 1 results):**

- For specific school data gaps: `"What is the Fraser Institute rating and EQAO score for [School Name] in [City]? Include the most recent year available, 5-year average if available, and Ontario rank."`
- For catchment/boundary data: `"School catchment zones and boundary maps for [Board Name] in [City]. Which neighborhoods fall within which school boundaries?"`
- For recent changes: `"Any new schools, school boundary changes, or program additions in [City] for [current year]. Include any schools that have recently opened, closed, or been reorganized."`

Also search for the **Fraser Institute Report Card** data specifically — it's the most widely used school ranking system in Ontario and many Canadian provinces. For areas outside Ontario/Canada, find the equivalent standardized rating system (e.g., GreatSchools ratings in the US, Ofsted in the UK).

**Compile into `[area]-schools.md`** with:

- Overview of school boards serving the area
- Every elementary school with ratings (EQAO %, Fraser rating, or equivalent)
- Every secondary school with ratings, programs offered (IB, AP, French Immersion, Gifted, STEM, Arts), and neighborhood served
- A comparison table of secondary schools ranked by rating
- Private/independent school options with tuition ranges
- Notes on specialized programs

**Source count check:** By the end of Phase 1, you should have **40+ unique source URLs** across both documents. If you're under 40, run additional targeted queries. List all sources at the bottom of each markdown file.

### Step 3: Data Normalization

Before moving to Phase 2, normalize the data:

- **School ratings**: Convert all ratings to a common 0–10 scale. Fraser Institute ratings are already 0–10. EQAO percentages can be noted separately. For areas without Fraser data, use whatever standardized rating system is available and note the conversion.
- **Home prices**: Use **median listing prices** in thousands (e.g., `1500` for $1.5M). If sources give ranges, use the midpoint for charting and note the range in descriptions.
- **Assign a "top school rating"** to each neighborhood based on the highest-rated school serving that area.
- **Calculate a price tier** for each neighborhood: Ultra-Luxury ($4M+), Premium ($2M–$4M), Mid-Range ($1M–$2M), Entry (<$1M). Adjust thresholds if the market warrants it (e.g., a market where everything is under $500K would need different tiers).

Save the normalized data in the markdown files or as a separate JSON reference — you'll need clean numbers for the charts.

---

## Phase 2: Report Synthesis (Interactive HTML)

Build a single self-contained HTML file. The default design is **Newsprint** (editorial newspaper aesthetic). Read `references/design-systems.md` for alternative options (Clean Modern, Corporate).

### Technology Stack

All loaded via CDN in the `<head>` — no build step, no local dependencies:

```html
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.7/dist/chart.umd.min.js"></script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=Lora:ital,wght@0,400;0,700;1,400&family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

For maps, also add:
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
```

### Tailwind Configuration (Newsprint)

Place this in the `<head>` immediately after the Tailwind CDN script:

```html
<script>
tailwind.config = {
  theme: {
    extend: {
      fontFamily: {
        headline: ['Playfair Display', 'Georgia', 'serif'],
        body: ['Lora', 'Georgia', 'serif'],
        ui: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      colors: {
        newsprint: '#F9F9F7',
        ink: '#111111',
        muted: '#E5E5E0',
        editorial: '#CC0000',
        gain: '#2E7D32',
      }
    }
  }
}
</script>
```

### Required `<style>` Block

The following CSS goes in a `<style>` tag in the `<head>`. These rules CANNOT be expressed in Tailwind alone and must be included exactly as shown:

```css
@media print {
  .no-print { display: none !important; }
  body { font-size: 11px; }
  section { page-break-inside: avoid; }
  canvas { max-height: 300px !important; }
}
html { scroll-behavior: smooth; }

body {
  background-color: #F9F9F7;
  background-image: radial-gradient(circle, #d4d4cf 1px, transparent 1px);
  background-size: 24px 24px;
}

/* Newsprint texture overlay */
.newsprint-texture { position: relative; }
.newsprint-texture::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 0;
}

/* Sharp corners everywhere — this is the Newsprint signature */
* { border-radius: 0 !important; }

/* Drop cap */
.drop-cap::first-letter {
  float: left;
  font-family: 'Playfair Display', Georgia, serif;
  font-size: 4.5rem;
  line-height: 0.8;
  padding-right: 0.15em;
  padding-top: 0.05em;
  font-weight: 900;
  color: #111111;
}

/* Tables */
table { border-collapse: collapse; width: 100%; }
th { position: sticky; top: 0; z-index: 1; }

/* Chart containers — THIS IS THE KEY RULE for chart sizing */
.chart-container { position: relative; width: 100%; max-width: 100%; }
@media (max-width: 768px) {
  .chart-container canvas { height: 300px !important; }
}

/* Hard offset shadow on hover for cards */
.card-newsprint {
  border: 1px solid #111111;
  transition: box-shadow 0.15s ease, transform 0.15s ease;
}
.card-newsprint:hover {
  box-shadow: 4px 4px 0px #111111;
  transform: translate(-2px, -2px);
}

/* Justified text */
.justified { text-align: justify; hyphens: auto; }

/* Ornamental divider */
.ornament {
  text-align: center;
  font-size: 1.25rem;
  letter-spacing: 0.5em;
  color: #999;
  padding: 1.5rem 0;
}

/* Section label style */
.section-label {
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 0.7rem;
  font-weight: 600;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: #777;
}

/* Inverted section */
.inverted { background-color: #111111; color: #F9F9F7; }

/* Figure captions */
.fig-caption {
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: #888;
  margin-top: 0.75rem;
}
```

### Body Tag

```html
<body class="font-body text-ink">
```

### Report Structure

The HTML report follows this section order. Each section has a labeled header, an introductory paragraph, and its content.

```
I.    Hero / Masthead (inverted section, newspaper-style title)
II.   Executive Summary / Key Findings (card grid)
III.  [Area] at a Glance (stat grid)
IV.   Neighborhood Price Map (Leaflet interactive map)
V.    Housing Price Analysis (bar chart, tables)
VI.   Neighborhood Profiles (filterable card grid)
VII.  School Rankings & Performance (bar charts, comparison table)
VIII. School-to-Price Correlation Analysis (scatter plot, analysis)
IX.   Specialized Programs Overview (vertical bar charts)
X.    Neighborhood Segmentation (cluster cards)
XI.   Appendix (source table, methodology notes)
```

### Section Layout Patterns (Tailwind)

**Section container pattern:**
```html
<section class="py-16 px-6 border-b border-muted newsprint-texture">
  <div class="max-w-screen-xl mx-auto relative z-10">
    <p class="section-label mb-2">Section I</p>
    <h2 class="font-headline font-black text-4xl md:text-5xl mb-2">Section Title</h2>
    <p class="font-body text-gray-500 italic mb-10">Subtitle or description</p>
    <!-- content here -->
  </div>
</section>
```

**Inverted section (for hero/masthead):**
```html
<section class="inverted py-16 md:py-24 px-6 relative overflow-hidden border-b-4 border-ink">
```

**Grid layout with border separators (NOT gap spacing):**
```html
<div class="grid md:grid-cols-2 gap-0 border border-ink">
  <div class="card-newsprint p-6 border-b md:border-b md:border-r border-ink">
    <!-- left column content -->
  </div>
  <div class="card-newsprint p-6">
    <!-- right column content -->
  </div>
</div>
```

**3-column grid:**
```html
<div class="grid md:grid-cols-3 gap-0 border border-ink">
  <div class="p-6 border-b md:border-b-0 md:border-r border-ink">...</div>
  <div class="p-6 border-b md:border-b-0 md:border-r border-ink">...</div>
  <div class="p-6">...</div>
</div>
```

**Chart-with-table side-by-side layout:**
```html
<div class="grid lg:grid-cols-8 gap-0 border border-ink">
  <div class="lg:col-span-5 p-4 border-b lg:border-b-0 lg:border-r border-ink">
    <div class="chart-container" style="min-height:470px;">
      <canvas id="myChart"></canvas>
    </div>
    <p class="fig-caption">Fig. 1 — Description</p>
  </div>
  <div class="lg:col-span-3 p-0">
    <table class="text-sm font-body">...</table>
  </div>
</div>
```

**Ornamental divider between sections:**
```html
<div class="ornament border-b-4 border-ink">◇ ◇ ◇</div>
```

**Callout/takeaway box:**
```html
<div class="border-l-4 border-editorial p-5 bg-white">
  <p class="font-body text-sm text-gray-700"><strong class="text-editorial">Key finding.</strong> Analysis text here.</p>
</div>
```

### Chart.js Implementation Guide

This is the most important section. Chart rendering issues are the #1 source of bugs. Follow this exactly.

**How charts are sized — the `.chart-container` + `min-height` pattern:**

Every chart canvas goes inside a `.chart-container` div with an inline `min-height` style. This is the ONLY way to size charts. Do NOT use `sizeChart()`, do NOT use `aspectRatio` for sizing, do NOT set height on the canvas element.

```html
<div class="chart-container" style="min-height:470px;">
  <canvas id="myChart"></canvas>
</div>
<p class="fig-caption">Fig. N — Description</p>
```

The `.chart-container` CSS class (defined in the style block above) provides `position: relative; width: 100%; max-width: 100%;`. The `min-height` inline style controls the chart height. The Chart.js option `maintainAspectRatio: false` (set on every chart) tells Chart.js to fill the container instead of computing its own size.

**Height guidelines for `min-height`:**
- Horizontal bar charts: `min-height:450px;` (adjust up to 500px for 15+ bars)
- Vertical bar charts: `min-height:420px;`
- Line charts: `min-height:450px;`
- Scatter/bubble charts: `min-height:450px;`
- Doughnut charts: `min-height:380px;`
- Stacked bar charts: `min-height:480px;`

These heights are generous enough for labels and legends to render cleanly without bleeding. When charts appear in 2-column or 3-column grids, the container naturally constrains the width and the `min-height` ensures enough vertical space.

**Total chart count:** Aim for **8–11 charts** total. More than 11 and the report becomes chart-heavy. Consolidate related metrics into one chart or move secondary data into tables.

**Chart.js global defaults — set once in the `<script>` block before any chart:**

```javascript
Chart.defaults.font.family = "'Lora', Georgia, serif";
Chart.defaults.font.size = 13;
Chart.defaults.color = '#555555';
Chart.defaults.borderColor = '#E5E5E0';
Chart.defaults.plugins.title.font = { family: "'Playfair Display', Georgia, serif", size: 18, weight: '900' };
Chart.defaults.plugins.title.color = '#111111';
Chart.defaults.plugins.legend.labels.font = { family: "'Inter', system-ui, sans-serif", size: 11 };
Chart.defaults.plugins.legend.labels.color = '#555555';
Chart.defaults.plugins.tooltip.titleFont = { family: "'Inter', system-ui, sans-serif", size: 12, weight: '600' };
Chart.defaults.plugins.tooltip.bodyFont = { family: "'JetBrains Mono', monospace", size: 12 };
Chart.defaults.plugins.tooltip.backgroundColor = '#111111';
Chart.defaults.plugins.tooltip.borderColor = '#111111';
Chart.defaults.plugins.tooltip.borderWidth = 1;
Chart.defaults.scale.ticks.font = { family: "'JetBrains Mono', monospace", size: 11 };
Chart.defaults.scale.grid.color = 'rgba(0,0,0,0.08)';
```

**Every chart MUST include these options:**
```javascript
responsive: true,
maintainAspectRatio: false,
```

**Example — a complete horizontal bar chart:**
```html
<div class="border border-ink p-4 mb-10">
  <div class="chart-container" style="min-height:470px;">
    <canvas id="priceChart"></canvas>
  </div>
  <p class="fig-caption">Fig. 1 — Median Home Prices by Neighborhood ($K)</p>
</div>
```
```javascript
new Chart(document.getElementById('priceChart'), {
  type: 'bar',
  data: {
    labels: ['Neighborhood A', 'Neighborhood B', 'Neighborhood C'],
    datasets: [{
      label: 'Median Price ($K)',
      data: [1200, 980, 750],
      backgroundColor: '#1B4F72',
      borderColor: '#111111',
      borderWidth: 1
    }]
  },
  options: {
    responsive: true,
    maintainAspectRatio: false,
    indexAxis: 'y',
    plugins: {
      title: { display: true, text: 'Median Home Prices by Neighborhood ($K)' },
      tooltip: { callbacks: { label: ctx => `$${ctx.raw}K` } }
    },
    scales: {
      x: { grid: { color: 'rgba(0,0,0,0.08)' } },
      y: { grid: { display: false } }
    }
  }
});
```

**Example — charts in a 2-column grid:**
```html
<div class="grid md:grid-cols-2 gap-0 border border-ink mb-10">
  <div class="p-4 border-b md:border-b-0 md:border-r border-ink">
    <p class="font-ui text-xs tracking-widest uppercase font-semibold mb-3">Chart Title Left</p>
    <div class="chart-container" style="min-height:420px;">
      <canvas id="chartLeft"></canvas>
    </div>
    <p class="fig-caption">Fig. N — Description</p>
  </div>
  <div class="p-4">
    <p class="font-ui text-xs tracking-widest uppercase font-semibold mb-3">Chart Title Right</p>
    <div class="chart-container" style="min-height:420px;">
      <canvas id="chartRight"></canvas>
    </div>
    <p class="fig-caption">Fig. N+1 — Description</p>
  </div>
</div>
```

**Doughnut charts:** Use `maintainAspectRatio: false` like all other charts. Place doughnuts in a 2-column grid to naturally constrain their width. Use `min-height:380px;` on the container.

**Bar sizing:** Always use `barPercentage` and `categoryPercentage` (percentage-based), never fixed `barThickness`. Typical values: `barPercentage: 0.82, categoryPercentage: 0.88` for horizontal bars; `barPercentage: 0.65, categoryPercentage: 0.8` for vertical bars.

### Table Styling (Tailwind)

Tables use Tailwind utility classes — no custom CSS needed:

```html
<div class="overflow-x-auto border border-ink">
  <table class="text-sm font-body">
    <thead class="bg-ink text-newsprint">
      <tr>
        <th class="text-left p-3 font-ui text-xs tracking-wider uppercase">Column</th>
        <th class="text-right p-3 font-ui text-xs tracking-wider uppercase">Value</th>
      </tr>
    </thead>
    <tbody>
      <tr class="border-b border-muted">
        <td class="p-2.5">Row label</td>
        <td class="p-2.5 text-right font-mono font-bold text-sm">$1,234K</td>
      </tr>
      <tr class="border-b border-muted bg-newsprint">
        <td class="p-2.5">Alternating row</td>
        <td class="p-2.5 text-right font-mono text-sm">$567K</td>
      </tr>
    </tbody>
  </table>
</div>
```

Key patterns:
- `bg-ink text-newsprint` for dark header rows
- `font-mono` for all numerical values
- `text-editorial` for negative/warning values
- `text-gain` for positive values
- Alternate `bg-newsprint` on even rows for zebra striping

### Leaflet Map Implementation

```html
<div class="border border-ink mb-10">
  <div class="bg-ink text-newsprint p-4 flex justify-between items-center">
    <h3 class="font-headline font-bold text-lg">Neighborhood Price Map</h3>
    <p class="font-ui text-xs tracking-widest uppercase text-gray-400">Interactive — click markers for details</p>
  </div>
  <div id="map" style="height:540px; filter: grayscale(70%) contrast(1.05);"></div>
</div>
```

```javascript
var map = L.map('map', {scrollWheelZoom: false}).setView([LAT, LNG], ZOOM);
L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', {
  attribution: '&copy; OpenStreetMap &copy; CARTO', maxZoom: 19
}).addTo(map);
```

For each neighborhood, add a `circleMarker` with `radius: 10`, `fillColor` based on price tier, and a popup showing name, price range, and top school.

### Stat Grid (Big Numbers)

```html
<div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-0 border border-ink">
  <div class="p-4 border-b border-r border-ink text-center">
    <p class="font-headline font-black text-3xl">42</p>
    <p class="font-ui text-xs tracking-widest uppercase text-gray-500 mt-1">Neighborhoods</p>
  </div>
  <!-- more stat cells -->
</div>
```

### Neighborhood Cards (JavaScript-generated)

Define neighborhood data as a JavaScript array and generate cards dynamically. Each card uses the `card-newsprint` class:

```javascript
var neighborhoods = [
  {name: 'Name', price: 1500, tag: 'family', schoolRating: 9.0,
   school: 'Top School Name', transit: 'GO Station', desc: 'Description...'},
  // ... more neighborhoods
];
```

### Avoiding Common Pitfalls

1. **JavaScript string escaping:** When inserting text with apostrophes into JS strings delimited by single quotes, use `\u2019` (Unicode right single quote) instead of a literal `'`. A single unescaped apostrophe will break the entire script block and render a blank page.

2. **Chart sizing:** ALWAYS use `.chart-container` with `min-height` inline style + `maintainAspectRatio: false`. NEVER use `aspectRatio` for non-doughnut charts. NEVER use a JavaScript `sizeChart()` wrapper function. NEVER set height on the `<canvas>` element directly.

3. **Doughnut charts:** Place in 2-column grids to naturally constrain width.

4. **Tailwind + custom CSS:** Use Tailwind for all layout and typography. Only use the `<style>` block for things Tailwind can't do (pseudo-elements, body background, `.chart-container`, hover transitions).

5. **Source count in the header:** Update the masthead to reflect the actual number of sources cited.

6. **Grid borders:** Use `gap-0 border border-ink` on the grid container and `border-r`, `border-b` on individual cells. This creates the Newsprint border-as-separator look. Do NOT use gap spacing.

---

## Phase 3: Review & Refinement

After generating the HTML report:

1. **Syntax check:** Run `node -e` to validate all JavaScript in the file parses without errors.
2. **Visual check:** Open the file and verify charts render correctly, map loads, cards filter properly.
3. **Data accuracy:** Spot-check 5+ data points against the original markdown sources.
4. **Tone check:** Ensure the language is analytical/research-oriented, not marketing/sales-oriented. No "buyers seeking" or "perfect for families" — instead use "neighborhoods characterized by" or "price-school correlation suggests."

---

## Analytical Tone Guide

This report is a research document, not a real estate listing. Follow these principles:

- **Describe, don't sell.** "Angus Glen commands the highest median prices in Markham" not "Angus Glen is the perfect choice for luxury buyers."
- **Use data language.** "The correlation coefficient (r ≈ 0.78) suggests..." not "Great schools mean great home values!"
- **Segment, don't recommend.** Section IX groups neighborhoods into analytical clusters (e.g., "High-Value Entry," "School-Premium Core," "Luxury Decoupling") rather than buyer profiles.
- **Acknowledge limitations.** Note that listing prices ≠ sale prices, that ratings capture academic outcomes but not culture, and that correlation ≠ causation.

---

## Design System Selection

Read `references/design-systems.md` for the full CSS specification of each available design system. Ask the user which style they prefer if they don't specify. The three options are:

1. **Newsprint** (default) — Editorial newspaper aesthetic. Playfair Display headlines, Lora body, Inter UI, JetBrains Mono data. Warm off-white background (#F9F9F7), black/red accent, zero border-radius, newsprint texture overlay, drop caps, ornamental dividers.

2. **Clean Modern** — Minimal, contemporary look. Inter for everything, white background, blue accent (#2563EB), subtle rounded corners (8px), card shadows, generous whitespace.

3. **Corporate** — Professional report style. Source Serif Pro headlines, system sans body, navy (#1e3a5f) and gold (#c9a84c) palette, formal table styling, executive summary emphasis.
