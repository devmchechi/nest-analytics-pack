# Chart Generator defaults

> Edit me after forking. Replace the example charts with the metrics you track.

## Charts (used by the daily-metrics workflow)

1. Daily signups, last 30 days, line chart with a 7-day moving average (dataset `signups`: `date`, `signups`)
2. Revenue by plan, this month vs. last month, horizontal bars (dataset `orders`: `date`, `plan`, `amount`)
3. Conversion rate vs. 3% target, last 8 weeks, line with a target line

## Preferences

- **Format:** PNG (also SVG when matplotlib is missing)
- **Brand accent color:** (none: use the Okabe-Ito palette)
- **Currency:** USD
- **Week starts on:** Monday
