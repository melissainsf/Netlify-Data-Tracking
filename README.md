# Netlify Content Performance Dashboard

External-facing content-performance dashboard for Netlify, powered by Virio.

## Tabs
1. **Performance Metrics Overview** — aggregate KPIs + trend charts (from Lineage analytics).
2. **By Post Performance** — sortable per-post table (from Lineage analytics).
3. **ICPs** — upload CSV lists; persisted in Supabase, shown as list widgets.

## Setup (in the Netlify project)
1. Connect this repo and deploy (root — no base directory needed).
2. Add environment variable **`LINEAGE_API_KEY`** = your Lineage API key.
3. (Optional) **`LINEAGE_ANALYTICS_URL`** — set the exact analytics endpoint if the
   default guesses don't connect. The function returns a debug sample to help find it.
4. (Optional) **`LINEAGE_ACCOUNT`** (default `netlify`) and **`LINEAGE_SINCE`** (default `2026-04-14`).

## Access
Google sign-in restricted to `@netlify.com` and `@virio.ai` accounts.

## Data
- Live content analytics sync from Lineage via `netlify/functions/lineage-analytics.js`.
- ICP CSV uploads stored in the Supabase table `netlify_icps`.
