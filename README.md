# Market Research Plugin

Real estate market research that produces comprehensive, interactive HTML reports analyzing neighborhoods, schools, and housing prices for any geographic area.

## What It Does

Give it a city or area, and it will:

1. **Research** — Run 8+ Tavily queries across 40+ sources to gather neighborhood profiles, school rankings, housing prices, transit data, and demographic info
2. **Compile** — Organize findings into structured markdown reference documents
3. **Synthesize** — Generate a single self-contained HTML report with Chart.js visualizations, Leaflet maps, data tables, and editorial-style analysis

## Usage

### Slash Command

```
/market-research Oakville
```

### Natural Language

Just ask Claude to research a neighborhood, city, or area:

- "Research Oakville neighborhoods and schools"
- "Do a full analysis of Richmond Hill — show me school-to-price correlation"
- "I want to compare neighborhoods in Burlington by school quality and home prices"

The skill triggers on mentions of neighborhood analysis, school ratings, housing reports, market research, or area comparisons.

## Design Systems

Three built-in visual styles for the HTML report:

- **Newsprint** (default) — Editorial newspaper aesthetic with Playfair Display headlines and zero border-radius
- **Clean Modern** — Minimal with blue accent, rounded corners, and card shadows
- **Corporate** — Professional navy/gold palette for executive presentations

## Installation

```bash
claude /install-plugin https://github.com/Casper-Studios/market-research-plugin
```

## Setup

No configuration needed. The skill uses Tavily research (available in Cowork) and generates self-contained HTML files with CDN-loaded dependencies.

## Example Output

See a live example: [The Markham Register](https://markham-report.pages.dev)

## License

MIT
