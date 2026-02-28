---
description: Run a neighborhood & school market research report
argument-hint: [city or area name]
---

Invoke the market-research skill to produce a comprehensive neighborhood and school analysis report for $ARGUMENTS.

Read the skill file at ${CLAUDE_PLUGIN_ROOT}/skills/market-research/SKILL.md and follow all three phases exactly:

1. **Phase 1**: Research the area using Tavily with 8+ queries across 40+ sources. Produce two markdown reference documents (neighborhoods + schools).
2. **Phase 2**: Synthesize a single self-contained interactive HTML report using the Newsprint design system (Tailwind CSS, Chart.js, Leaflet.js) following the exact template patterns in the skill.
3. **Phase 3**: Validate JavaScript syntax, spot-check data accuracy, and verify analytical tone.

Save the final HTML report to the user's workspace folder.
