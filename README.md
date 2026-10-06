# Analytics Pack

From raw exports to a report your team trusts. Data Fetcher loads, validates and profiles your data; Chart Generator makes honest, labeled charts; Report Writer turns them into a short KPI report where every number comes from a saved script. The **Daily Metrics** workflow runs all three.

## Agents

| Agent                                               | What it does                                                                                          | Network                                    |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| [Data Fetcher](agents/data-fetcher/README.md)       | Loads CSV/JSON from the working folder or allowlisted URLs; cleans, profiles and flags quality issues | `raw.githubusercontent.com` (add your own) |
| [Chart Generator](agents/chart-generator/README.md) | PNG/SVG charts with the right type, honest axes and takeaway titles; matplotlib or plain-Python SVG   | none                                       |
| [Report Writer](agents/report-writer/README.md)     | KPI report against targets: TL;DR, what changed, watch list, data notes                               | none                                       |

## Workflow: Daily Metrics

`workflows/daily-metrics.yaml`:

1. **fetch** (Data Fetcher): loads the sources in its `instructions.md`, cleans and profiles them, and ends its reply with a Handoff section holding the clean data as CSV text (daily aggregates for datasets over 1,000 rows).
2. **charts** (Chart Generator): saves that CSV into its own folder and makes the charts in its `instructions.md`, kept in `~/.nest/local/work/chart-generator/charts/`. If this step fails, the report is written without charts.
3. **report** (Report Writer): computes the KPIs and targets in its `instructions.md` from the same CSV and writes the report, which it returns in its reply and saves to `~/.nest/local/work/report-writer/reports/`.

Before running it, fork the three agents and replace the example sources, charts and KPIs with your own.

## Getting data in

- **Files:** export from your analytics tool, database or spreadsheet into Data Fetcher's folder, `~/.nest/local/work/data-fetcher/data/raw/`.
- **URLs:** Data Fetcher can only reach hosts on its allowlist, which out of the box is just `raw.githubusercontent.com`. To add yours, fork Data Fetcher and add the host to `network.allow` in its `skill.md`:

  ```yaml
  network:
    allow:
      - host: raw.githubusercontent.com
      - host: data.example.com
  ```

  API keys aren't supported out of the box. Export to a file instead.

## Working folders

Every agent has its own working folder, `~/.nest/local/work/<agent-id>/` on your computer (`%USERPROFILE%\.nest\local\work\<agent-id>\` on Windows), which it sees as its current directory. Agents can't see each other's folders. Put input files in the folder of the agent that reads them; in workflows, results pass from step to step in the agents' replies, never through files.

## Capabilities

- **Tools:** shell commands (Python processing and plotting), reading and writing files, listing folders. Shell commands and file writes always ask for your approval first.
- **Network:** only Data Fetcher, only `raw.githubusercontent.com` until you add hosts.
- **Pilots:** none.
- **Typical cost:** about $0.05 to $0.45 per Daily Metrics run on paid models.

## Fork to customize

Installed agents are read-only. **Fork** an agent in Nest to get your own editable copy. Each agent's `instructions.md` (marked "Edit me after forking") holds its sources, charts, KPIs and targets.

## License

MIT. See [LICENSE](LICENSE).
