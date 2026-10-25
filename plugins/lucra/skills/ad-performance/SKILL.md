---
name: ad-performance
description: Reports how a brand's creator ads perform in Lucra (spend, attributed sales, return by day, campaign, creator, ad or platform), charts the trend, and pauses or resumes campaigns. Use when the user asks how ads or creators are doing, who the top creators are, what's spending without returning, or to pause, resume or compare campaigns.
---

# Creator ad performance in Lucra

## Numbers

- Results come from `/v1/analytics` (Lucra's own attribution). Query: `from`, `to` (ISO dates), optional `mode` (`paid` default, or `organic` for views), `platform` (`meta|tiktok|google|snapchat`), `campaign`, `creator`, `program`, and `group` to split by.
- Totals and rankings: `tally_lucra` path `/v1/analytics` with `query {"group": "creator", "from": ..., "to": ...}`, `fields ["group.creator"]`, `sum ["revenue", "spend"]`. Swap `creator` for `campaign`, `ad` or `platform`.
- Over time: `tally_lucra` with `fields ["date:day"]` (or `:week`) and `sum ["spend", "revenue"]`, then `chart` type `line` with exactly those values (unit `currency`, values in cents).
- Default window: the last 7 days unless the user says otherwise.

## Answer shape

1. Lead with the headline: spend, attributed sales and return (sales ÷ spend, e.g. **3.2x**), and the change vs the previous window when you read both.
2. Show the records behind it: for top creators or campaigns, `read_lucra` `/v1/creators` or `/v1/campaigns` and show them in rank order.
3. Flag what looks off kindly ("Heads up, return on the Spring campaign halved").

## Pause, resume, archive

1. `read_lucra` `/v1/campaigns/:id` for its `version`.
2. `change_lucra` `PATCH /v1/campaigns/:id` body `{"status": "paused" | "live", "version": <version>}`.
3. Archiving (`"status": "archived"`) ends the campaign: confirm with the user first.
4. Campaigns that need attention: `read_lucra` `/v1/campaigns` with `{"status": "needs_attention"}`; each says why.
