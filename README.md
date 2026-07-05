# Premier League 2026/27 Predictor

A family score-prediction game for the 2026/27 Premier League season. Predict all ten scorelines each gameweek. Each week has its own winner, and every point rolls into a season table.

**Live site:** _add your GitHub Pages URL here once published_

## How it works
- One page (`index.html`). Gameweeks release one at a time; picks lock at 7:30pm on the Friday of each gameweek.
- Scoring: 3 for the exact score, 1 for the right result, 0 otherwise.
- Data lives in a Google Sheet behind a Google Apps Script web app (`Code.gs`). Setup is in `SETUP-PL.md`.

## Files
- `index.html` — the app (predictions, leaderboard, results). This is the site.
- `premier-league-24-25.jpg` — header image (keep it next to index.html).
- `Code.gs` — Google Apps Script backend, pasted into the sheet's script editor.
- `SETUP-PL.md` — plain-English setup guide.
- `pl_fixtures.json` — the full 2026/27 fixture list.
