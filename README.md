# MMTrades — Trades by Month

A line chart of trade volume from the Notion **BACKTESTING** database, grouped by calendar month (America/New_York). Shows total trades logged per month plus quick stats for busiest month, quietest month, and monthly average.

## Setup

1. **Add the `NOTION_TOKEN` secret** to this repo: Settings → Secrets and variables → Actions → New repository secret. Use the same integration token already used on the other `mmtrades-*` repos (it needs read access to the `BACKTESTING` database).
2. **Enable GitHub Pages**: Settings → Pages → Source: "Deploy from a branch" → Branch: `main`, folder `/ (root)`.
3. **Run the sync once manually**: Actions tab → "Sync Notion trades" → Run workflow. After that it runs automatically every 5 minutes.

Your page will be live at `https://<your-username>.github.io/<this-repo-name>/`.

## Files

- `index.html` — the chart itself (line chart, dark/light theme, self-contained).
- `sync.js` — pulls the `Date` property from the BACKTESTING data source and rewrites the `ENTRY_TIMESTAMPS_UTC` array between the `SYNC_MARKER_START` / `SYNC_MARKER_END` comments in `index.html`. Also writes `.sync-debug.json` on every run (success or failure) so sync issues are diagnosable without needing raw Action logs.
- `.github/workflows/sync.yml` — runs `sync.js` on a schedule and commits the result.
