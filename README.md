# nanci-cost-dashboard

Single-page dashboard for Jeff Livingston's Nanci VCoS daily cost tracking.

**Live:** https://jbliving06.github.io/nanci-cost-dashboard/

## What it shows

- **Daily spend, last 30 days** — stacked line chart, Anthropic / ElevenLabs / Twilio / other
- **Month-to-date vs $500 ceiling** — progress bar that turns warn at 80%, bad at 100%
- **Vendor breakdown** — MTD doughnut
- **Calls per day** — bar chart, derived from Twilio usage records

## How data flows

`~/VCOS/cost_tracker.gs::ct_publishDashboardJson_` runs daily at the end of
`ct_dailyPoll` (~7:15 AM ET). It reads the last 30 days from the Notion Cost
Tracking database, computes the per-vendor / per-day rollup, and PUTs the
result to `data.json` in this repo via the GitHub Contents API.

The HTML is a single self-contained file (Chart.js from CDN). No build step,
no server. GitHub Pages serves it from `main`.

## Local edits

Only edit `index.html` and this README directly. `data.json` is overwritten
daily by the GAS publisher — any local edits will be clobbered on the next
`ct_dailyPoll` run.
