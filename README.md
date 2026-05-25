# Green Hat Championship Scoreboard

A single-file HTML golf trip scoring app. No server, no dependencies — open `golf-trip.html` directly in a browser.

## Features

- **Trips** — create and switch between named golf trips (e.g. "Green Hat 2025")
- **Rounds** — add rounds with course details (name, rating, slope, date) and players with handicaps
- **Course library** — 3 pre-loaded WA courses (Apple Tree, Wine Valley, Moses Pointe) with full hole-by-hole par/handicap/yardage data; custom courses supported via JSON input
- **Scorecards** — enter scores hole by hole; cells color-code by result (eagle/birdie/par/bogey/double/triple+); desktop horizontal layout and mobile vertical layout with large tap targets
- **Handicap-adjusted net scores** — hole handicap allocation method (strokes distributed across hardest holes)
- **Leaderboard** — overall standings and round-by-round breakdown, togglable between gross and net
- **Line chart** — running cumulative score vs par across all holes and rounds, per player
- **Persistence** — all data saved to `localStorage`; migrates legacy `golfTrip` key automatically

## Tech

Single HTML file: vanilla JS, CSS custom properties, SVG chart. No build step, no frameworks.

## Data model (localStorage key: `golfApp3`)

```json
{
  "trips": [
    {
      "id": "uid",
      "name": "Green Hat 2025",
      "rounds": [
        {
          "id": "uid",
          "date": "YYYY-MM-DD",
          "course": { "name": "", "rating": 74.3, "slope": 136, "holes": [...] },
          "players": [{ "name": "", "handicap": 10 }],
          "scores": { "PlayerName": [null, 4, 5, ...] }
        }
      ]
    }
  ],
  "activeTripId": "uid"
}
```

Scores are stored as **strokes relative to par** (e.g. `-1` = birdie, `0` = par, `1` = bogey).
