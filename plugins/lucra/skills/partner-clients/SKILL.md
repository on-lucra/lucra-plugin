---
name: partner-clients
description: Works across an agency's or partner's client brands in Lucra (lists clients, compares spend and results by client, and acts inside one client's workspace). Use when the user is a partner or agency asking about their clients, their book of business, or wants to do something for a specific client brand.
---

# Work across partner clients in Lucra

## Clients

- The partner's clients: `read_lucra` `/v1/relationships` (each relationship's `counterparty` is the brand, with its `acct_…` ID and status).
- The book at a glance: `tally_lucra` `/v1/relationships` with `fields ["status"]`, then `chart` type `donut`.

## Act inside a client

Pass the client's `acct_…` ID as `account` on any tool call (`read_lucra`, `change_lucra`, `tally_lucra`). Everything then runs in that brand's workspace with the partner's access there.

Examples:
- "What's waiting for Acme?" → the review-creator-work lists with `account: "acct_…"` (Acme's ID from `/v1/relationships`).
- "Spend by client this month" → for each active client, `tally_lucra` `/v1/analytics` with that `account`, then one `chart` type `bar` comparing them.

## Rules

- Say which client you're working in before any change ("In Acme: paused Summer UGC").
- A partner's access in a client can be narrower than the brand's own team; a 403 means their role there can't do it.
