# Data Fetcher

Gets your data into clean, analysis-ready shape. It loads CSV, TSV, JSON and JSON Lines from your working folder, or downloads them from allowlisted URLs. It detects encodings and types, profiles every column, flags quality problems (duplicates, gaps, impossible values, schema changes since the last run), cleans conservatively, and documents every change.

## What it needs

**Working folder:** every agent has its own, and this one's is `~/.nest/local/work/data-fetcher/` on your computer (`%USERPROFILE%\.nest\local\work\data-fetcher\` on Windows). The agent sees it as its current directory, so a path like `./notes/` means `~/.nest/local/work/data-fetcher/notes/`. Other agents can't see this folder; in workflows, results pass between agents in their replies.

- Data files in `./data/raw/`, i.e. `~/.nest/local/work/data-fetcher/data/raw/` (exports from your analytics tool, database, spreadsheet, and so on), or sources listed in `instructions.md`.
- For downloads: the host must be on the agent's network allowlist. Out of the box only `raw.githubusercontent.com` (public files on GitHub) is allowed. To add your own:
  1. Fork the agent in Nest (installed agents are read-only until forked).
  2. In the fork's `skill.md`, add the host under `network.allow`:
     ```yaml
     network:
       allow:
         - host: raw.githubusercontent.com
         - host: data.example.com
     ```
  3. Add the URL to the **Sources** list in `instructions.md`.
- APIs that need keys aren't supported out of the box. Export the data to a file instead.

## What it produces

- `./data/clean/<name>.csv`: tidy, typed, with ISO dates.
- `./data/profile.json`: a profile of each dataset, its issues, and the cleaning changes made.
- `./data/scripts/fetch_<name>.py`: the re-runnable loading script.
- A short quality report in chat. When a workflow asks, the reply ends with a Handoff section holding the clean data as CSV text (daily aggregates for large datasets), which is how Chart Generator and Report Writer receive it.

## Example prompts

- "Load everything in ./data/raw and tell me what's wrong with it."
- "Fetch https://raw.githubusercontent.com/datasets/gdp/master/data/gdp.csv and profile it."
- "Did the schema of orders.csv change since yesterday?"

## Capabilities in plain language

| Capability                           | Why                                                                      |
| ------------------------------------ | ------------------------------------------------------------------------ |
| Runs shell commands (asks first)     | Downloads with `curl` and processes with Python                          |
| Reads files and lists folders        | Finds and reads your data files                                          |
| Writes files (asks first)            | Writes clean data, the profile and scripts. Raw files are never changed. |
| Network: `raw.githubusercontent.com` | Public datasets on GitHub. Add your own hosts after forking.             |
