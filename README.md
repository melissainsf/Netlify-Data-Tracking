# Netlify Content Performance Dashboard

External-facing content-performance dashboard for Netlify, powered by Virio.
Live at https://viriodashboard.netlify.app/

## Tabs
1. **Mathias · Overview** — KPIs, trend charts, discovery, engagement breakdown,
   audience demographics and the ICP engagement report for Mathias Biilmann Christensen.
2. **Mathias · By Post** — sortable per-post table.
3. **RTL · Overview** — the same view for Richard Terry-Lloyd.
4. **RTL · By Post** — the same per-post table for Richard.
5. **Leaderboard** — head-to-head T-chart, Mathias vs Richard, for the most recent
   period both people have a report for. Growth / Engagement / Reach, leader highlighted.
6. **ICPs** — the ICP engager lists from `/data`, plus any CSV uploaded here
   (uploads are stored in Supabase and shared with everyone who opens the dashboard).

## Data
All analytics are baked into `index.html`, so a refresh is a GitHub push and
nothing else — no external data store and no API keys.

Each person has one or more **reports** in `PEOPLE`. A report is one LinkedIn
"Aggregate Analytics" export. Reports never overlap and are never stitched
together, so every figure on screen comes from a single export and reconciles
with what LinkedIn shows.

Currently loaded:

| Person  | Report            | Source                          |
| ------- | ----------------- | ------------------------------- |
| Mathias | August 2026       | LinkedIn export, Aug 1 – Aug 31 |
| Mathias | Apr 13 – Jul 27   | LinkedIn export                 |
| RTL     | August 2026       | LinkedIn export, Aug 1 – Aug 31 |

### Adding next month
1. In LinkedIn: **Analytics → Export**, pick the month, download the `.xlsx`
   for each person.
2. Add a report object to that person's `reports` array in `index.html`, newest
   first. Fields come straight from the export's sheets:
   - `impr` / `eng` — the ENGAGEMENT sheet's two daily columns
   - `fNew` — the FOLLOWERS sheet's daily column; `totFollowers` is its header total
   - `discovery` — the DISCOVERY sheet plus the in/out-of-network split
   - `demo` / `contentDemo` — the AUDIENCE and CONTENT DEMOGRAPHICS sheets
   - `posts` — the TOP POSTS sheet, merging its engagements and impressions lists
     on Post URL; the optional 5th element is the post's opening line, used as its title
   - `breakdown` — reactions / comments / reposts / saves / sends, which live on
     LinkedIn's Engagement card rather than in the export
3. The period picker, the By Post tab and the Leaderboard pick it up automatically.
   The Leaderboard compares the newest period both people have.

### ICP reports and lists
- The narrative report per person is `ICP_MATHIAS` / `ICP_RTL` in `index.html`,
  taken from the periodic Lineage ICP Engagement Report PDF. Replace in place.
- The full engager lists are CSVs committed under `data/`, referenced by
  `icpFile` on each person and rendered (filterable, downloadable) on the ICPs tab.

## Access
Google sign-in restricted to `@netlify.com` and `@virio.ai` accounts.
