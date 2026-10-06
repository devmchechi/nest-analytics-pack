# Data Fetcher defaults

> Edit me after forking. List your own data sources here; the daily-metrics workflow uses this list.

## Sources

- `./data/raw/*.csv`: exports you drop in (e.g. daily signups, orders, traffic)
- `./data/raw/*.json`
- Example public URL (remove or replace): `https://raw.githubusercontent.com/owid/covid-19-data/master/public/data/latest/owid-covid-latest.csv`

To fetch from other hosts (your own API or data warehouse export URL), fork the agent and add each host to `network.allow` in `skill.md`.

## Conventions

- **Date column names:** `date`, `day`, `created_at`
- **Ambiguous date format:** (none; e.g. `%d/%m/%Y` if your exports are day-first)
- **Key columns for duplicate checks:** (e.g. `orders.csv: order_id`)
- **Missing values:** leave them as they are (don't fill)
