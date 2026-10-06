# Chart Generator

Makes charts that answer one question at a glance and can't mislead. It picks the right chart type, computes the takeaway before writing a title, labels axes and units, uses a colorblind-safe palette, and saves the script for every chart so you can re-run or tweak it.

## What it needs

**Working folder:** every agent has its own, and this one's is `~/.nest/local/work/chart-generator/` on your computer (`%USERPROFILE%\.nest\local\work\chart-generator\` on Windows). The agent sees it as its current directory, so a path like `./notes/` means `~/.nest/local/work/chart-generator/notes/`. Other agents can't see this folder; in workflows, results pass between agents in their replies.

- Data pasted into chat (in the Daily Metrics workflow, Data Fetcher's clean data arrives as CSV text in the message), or CSV/JSON files in its own `./data/` folder.
- What to chart, from your prompt or the **Charts** list in `instructions.md` (edit after forking).
- It uses matplotlib when the runtime has it. Otherwise it draws SVG charts with plain Python, so no install is needed. No internet access.

## What it produces

- `./charts/<date>-<name>.png` (or `.svg`) and `./charts/scripts/<name>.py`.
- `./charts/index.md`: titles, alt text and key numbers for each chart.

## Example prompts

- "Chart daily active users from ./data/dau.csv for the last 90 days."
- "Compare revenue by region this quarter vs. last quarter."
- "Make the charts in my instructions for today."
- "Show the distribution of order values and point out outliers."

## Capabilities in plain language

| Capability                       | Why                                     |
| -------------------------------- | --------------------------------------- |
| Runs shell commands (asks first) | Runs the Python plotting scripts        |
| Reads files and lists folders    | Reads your data and its profile         |
| Writes files (asks first)        | Saves charts and scripts to `./charts/` |
| Network                          | None                                    |
