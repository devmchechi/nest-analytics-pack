# Report Writer

Writes the metrics report your team actually reads: a three-bullet TL;DR, a KPI table against targets, what changed and where it came from, a watch list, data notes and open questions. Every number comes from a script it runs and saves. It never eyeballs numbers or makes up explanations.

## What it needs

**Working folder:** every agent has its own, and this one's is `~/.nest/local/work/report-writer/` on your computer (`%USERPROFILE%\.nest\local\work\report-writer\` on Windows). The agent sees it as its current directory, so a path like `./notes/` means `~/.nest/local/work/report-writer/notes/`. Other agents can't see this folder; in workflows, results pass between agents in their replies.

- Data pasted into chat, or CSV files in its own `./data/` folder. In the Daily Metrics workflow it receives Data Fetcher's clean data and Chart Generator's chart list in the message. Charts stay in Chart Generator's folder, and the report refers to them by file name.
- Your KPI definitions, targets and thresholds in `instructions.md` (edit after forking).
- Optional context in `./reports/context.md`: launches, outages, campaigns, holidays. This is the only place it takes "why" from.

No internet access.

## What it produces

- `./reports/<date>-<name>.md` with references to the charts, plus the full report in the reply.
- `./reports/scripts/compute_<date>.py`: the calculations behind every number.

## Example prompts

- "Write today's metrics report."
- "Weekly report for last week, for the board, with less detail."
- "Why did revenue drop yesterday? Break it down by plan and country."

## Capabilities in plain language

| Capability                       | Why                                              |
| -------------------------------- | ------------------------------------------------ |
| Runs shell commands (asks first) | Runs the Python script that computes the numbers |
| Reads files and lists folders    | Reads data, charts, context and past reports     |
| Writes files (asks first)        | Saves reports to `./reports/`                    |
| Network                          | None                                             |
