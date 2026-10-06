# Report Writer defaults

> Edit me after forking. Replace the example KPIs with your own definitions and targets.

- **Report name:** Daily Metrics
- **Audience:** founders and team leads; avoid statistical jargon
- **Reporting period:** yesterday (daily data); compare with the day before and the same weekday last week

## KPIs

| KPI             | Definition                        | Source            | Target     | Watch if | Off track if |
| --------------- | --------------------------------- | ----------------- | ---------- | -------- | ------------ |
| Signups         | count of rows per `date`          | dataset `signups` | 120/day    | < 100    | < 80         |
| Revenue         | sum of `amount` per `date`        | dataset `orders`  | $4,000/day | < $3,500 | < $3,000     |
| Conversion rate | orders / signups, trailing 7 days | both files        | 3.0%       | < 2.7%   | < 2.4%       |

- **Segments to break changes down by:** `plan`, `country`
- **Context file:** `./reports/context.md` (add launches, outages and campaigns here)
