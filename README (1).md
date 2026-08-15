# 11u Lineup Card Generator (Enhanced UI)

A single-file, browser-based tool for building fair, rule-compliant baseball lineup cards for an 11U team. No installation, no server, no build step — download the HTML file and open it in a browser.

Built for the **Glenview Fall League** 11U rules (7-inning games, 3-inning pitcher max), but easy to adapt for other leagues.

## Features

**Roster Settings**
- Attendance tracking per game
- Player ratings: Defense, Overall Hitting, Power, Speed, Pitcher Control, Pitcher Speed (1–10 scale, with an N/A option)
- Pitcher Availability (Innings) and manual Pitcher/Catcher inning locks
- Excluded Positions (positions a player should never play)
- Primary Positions (reference-only notes on a player's best spots)
- Three optional bias toggles: favor better defenders at key positions, sit weaker defenders more often, and/or sit weaker defenders specifically in late innings
- Export/Import roster settings as a JSON file, so you can share a full roster configuration with a co-coach

**Lineup Generation**
- Builds a complete 7-inning fielding lineup plus batting order automatically
- Batting order defaults to speed/contact hitters first, power hitters next, then the rest by hitting rating — fully drag-and-drop adjustable afterward
- **Strict bench fairness**: no two players' total bench (OUT) innings can differ by more than 1, guaranteed — the app will never sit one player extra just to force a lineup through
- Pitcher innings are always consecutive, capped at each player's set availability
- Every inning gets exactly one catcher, at least 2 infield innings per player, and no duplicate positions per inning
- If generation can't succeed while keeping bench time fair, the app tells you *why* — naming the specific player, position, or inning that's the bottleneck, with suggested fixes

**Lineup Card**
- Drag-and-drop batting order and reserve pitcher order
- Manual position overrides per player, per inning
- Live rule-violations panel
- Innings Sat Summary (who sat how many innings, most to fewest)
- One-click, print-ready PDF export designed to fit on a single page

**Other**
- Dark, high-contrast UI themed around night-game stadium lighting
- All settings auto-save to the browser's local storage and reload automatically next time you open the file
- Works fully offline once downloaded — no external dependencies, no analytics, no network calls

## Getting Started

1. Download the `.html` file from this repo (or clone the repo).
2. Open it in a modern browser (Chrome recommended for the best PDF export experience).
3. Go to **Roster Settings**, mark who's attending, and fill in ratings/pitching info for your roster.
4. Click **Generate lineup**.
5. Review the **Lineup Card** tab, drag to adjust the batting order if you like, then click **Download PDF**.

No build tools, no `npm install`, no server required — it's a single self-contained HTML file.

## Data & Privacy

Everything is stored locally in your browser (`localStorage`), tied to that specific browser and that specific copy of the file. Nothing is ever sent to a server — there isn't one.

This has two practical implications:
- If you clear your browser data, use a different browser, or open the file on another device, your saved roster won't be there. Use **Export Roster Settings to Share** to download a backup/transfer file, and **Import** to load it back in (on this device or another).
- If you want to hand this app to a co-coach with your roster pre-filled, send them both the `.html` file and an exported `.json` settings file.

## Known Limitations

- **Overall Hitting, Power, Speed, Pitcher Control, and Pitcher Speed ratings are informational only.** Only **Defense Rating** currently feeds into the generation algorithm (position assignment and the bench biases). The others are there for your own reference and for building out the batting order priority (Hitting/Power/Speed already factor into batting order).
- Designed around a single team's roster at a time — there's no multi-team switching built in.
- PDF export opens a new browser tab and relies on `window.print()`, so pop-ups must be allowed for the page/file. If you're viewing the app inside an embedded preview (like a chat tool's file viewer) rather than a full browser tab, pop-up blocking can behave inconsistently — open the downloaded file directly in your browser for the most reliable PDF export.
- Tested primarily in Chrome. Other modern browsers should work but haven't been extensively verified.

## Suggested Repo Structure

Beyond this README, a few things worth adding if you're publishing this on GitHub:

- **`LICENSE`** — pick one (MIT is a common, permissive default for a small utility like this) so it's clear others can use/fork it.
- **Rename the main file to `index.html`** — if you enable **GitHub Pages** on the repo, this lets you (and your co-coaches) open the live app directly from a URL instead of downloading and opening a local file each time. Note that browser local storage and PDF pop-up behavior both work more predictably when the app is loaded from a real URL rather than a local `file://` path, so this is worth doing even if you don't share the link widely.
- **`CHANGELOG.md`** — a running list of what's changed between versions. Handy once you're a season or two in and can't remember what you tweaked and why.
- **`.gitignore`** — even for a single-file project, a minimal one keeps OS clutter (`.DS_Store`, `Thumbs.db`, editor swap files) out of the repo.
- **A `/screenshots` folder** — one or two images of the Roster Settings and Lineup Card tabs embedded in this README make the repo much easier to understand at a glance for anyone who finds it.
- **A sample exported settings file** (e.g. `sample-roster-settings.json`) — useful as a template for new users, and as a quick sanity check that Import still works after future edits.

## License

Add your preferred license here (see "Suggested Repo Structure" above).
