---
name: partner-clients
description: Works across an agency's or partner's client brands in Lucra (lists clients, compares spend and results by client, and acts inside one client's workspace). Use when the user is a partner or agency asking about their clients, their book of business, or wants to do something for a specific client brand.
---

# Work across partner clients in Lucra

## Clients

- The partner's clients: `brands_find` (each brand with its `acct_…` ID; brands whose relationship ended are marked).
- The book at a glance: `tally` with `list "brands_find"` and `fields ["status"]`.

## Act inside a client

Pass the client's `acct_…` ID as `account` on any tool call. Everything then runs in that brand's workspace with the partner's access there.

Examples:
- "What's waiting for Acme?" → the review-creator-work lists with `account: "acct_…"` (Acme's ID from `brands_find`).
- "Spend by client this month" → for each active client, `tally` with `list "ad_results"` and that `account`, then one short table comparing them.

## Rules

- Say which client you're working in before any change ("In Acme: paused Summer UGC").
- A partner's access in a client can be narrower than the brand's own team; a 403 means their role there can't do it.
