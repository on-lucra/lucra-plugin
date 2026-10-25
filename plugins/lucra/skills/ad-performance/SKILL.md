---
name: ad-performance
description: Reports how a brand's creator ads perform in Lucra (spend, attributed sales, return by day, campaign, creator, ad or platform), charts the trend, and pauses or resumes campaigns. Use when the user asks how ads or creators are doing, who the top creators are, what's spending without returning, or to pause, resume or compare campaigns.
---

# Creator ad performance in Lucra

## Numbers

- Results come from `ad_results` (Lucra's own attribution). Its `query`: `from`, `to` (ISO dates), optional `mode` (`paid` default, or `organic` for views), `platform` (`meta|tiktok|google|snapchat`), `campaign`, `creator`, `program`, and `group` to split by.
- Totals and rankings: `tally` with `list "ad_results"`, `query {"group": "creator", "from": ..., "to": ...}`, `fields ["group.creator"]`, `sum ["revenue", "spend"]`. Swap `creator` for `campaign`, `ad` or `platform`.
- Over time: `tally` with `fields ["date:day"]` (or `:week`) and `sum ["spend", "revenue"]`, then `chart` type `line` with exactly those values (unit `currency`, values in cents).
- Default window: the last 7 days unless the user says otherwise.

## Answer shape

1. Lead with the headline: spend, attributed sales and return (sales ÷ spend, e.g. **3.2x**), and the change vs the previous window when you read both.
2. Show the records behind it: for top creators or campaigns, `creators_find` or `campaigns_find` each, in rank order.
3. Flag what looks off kindly ("Heads up, return on the Spring campaign halved").

## Pause, resume, archive

1. `campaigns_find` with its `id` for the `version`.
2. `campaigns_update` with `id` and `body {"status": "paused" | "live", "version": <version>}`.
3. Archiving (`"status": "archived"`) ends the campaign: confirm with the user first.
4. Campaigns that need attention: `campaigns_find` with `query {"status": "needs_attention"}`; each says why.
