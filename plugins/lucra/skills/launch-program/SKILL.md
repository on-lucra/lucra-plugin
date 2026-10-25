---
name: launch-program
description: Creates a Lucra creator program (UGC or paid creator ads) from a short brief, invites creators to it, and opens it to the Lucra Network. Use when the user wants to start a creator program, find creators for a launch, write a brief, or invite creators.
---

# Launch a creator program in Lucra

## Create

Work out everything you can from what the user said, default the rest, create it, show it, then offer changes. Ask at most two questions, one at a time, and only for what's required and truly unknown.

1. You need:
   - `type`: `organic` (creators post on their own accounts, paid per video or per 1,000 views) or `paid_ads` (the brand runs creators' videos as ads, paid a percent of ad spend).
   - `name`: pick a good one from their product or goal; they can rename it.
   - `pay`: ask in the program's own terms if they didn't say it. The `programs_create` input schema has its exact shape.
2. `programs_create` with `body` holding `visibility: "invite"` (a draft nobody else sees), the `brief` (what to film, the key message, what to avoid), `platforms`, `type`, `name` and `pay`.
3. The new program shows as a card. Offer to open it to the Lucra Network (`programs_update` with `body {"visibility": "network", "version": <version>}`) or tweak the brief.

Leave optional settings (limits, schedules, agreements, files) out unless the user brings them up.

## Invite creators

- Find creators in their roster: `creators_list` with `query {"q": "<name or handle>"}`.
- Invite one: `applications_create` with `body {"program": "prog_…", "creator": "crtr_…"}`.

## Brief tips

A strong brief names: the product and its one key benefit, the hook in the first 2 seconds, what to show, the call to action, and what to avoid (competitor mentions, claims). Two to five short bullets beat a paragraph.
