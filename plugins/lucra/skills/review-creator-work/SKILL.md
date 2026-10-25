---
name: review-creator-work
description: Reviews what's waiting on a brand in Lucra (creator applications to programs, creator videos to approve, sample requests, campaigns that need attention) and approves, rejects or requests changes. Use when the user asks what needs their attention, who applied, which videos are waiting, or to approve or reject creators or content.
---

# Review creator work in Lucra

## What needs attention

Read each list that applies, show it, and say in one line what to do about it:

- Applications waiting: `applications_list` with `query {"status": "pending"}`
- Videos waiting for review: `submissions_list` with `query {"status": "pending"}`
- Sample requests: `samples_list` with `query {"status": "pending"}`
- Campaigns with a problem: `campaigns_list` with `query {"status": "needs_attention"}`

Lead with the count that matters most ("3 videos and 2 applications are waiting"). If nothing is waiting, say so in one cheerful line.

## Approve, reject or request changes

1. Retrieve the record (`applications_retrieve` or `submissions_retrieve` with its `id`) for its current `version`.
2. Update it:
   - Application: `applications_update` with `id` and `body {"status": "approved" | "rejected", "version": <version>}`
   - Video: `submissions_update` with `id` and `body {"status": "approved" | "rejected" | "revision_requested", "note": "<what to change>", "version": <version>}`. A revision request needs a short, specific note.
3. Name what you did ("Approved Maya's video for Summer UGC"), never "the first one".

Routine single approvals and rejections need no extra confirmation when the user asked for them. Confirm before approving or rejecting more than three at once, and before any approval that pays the creator.

## Examples

- "Who applied this week?" → `applications_list` with `query {"status": "pending", "createdAfter": "<7 days ago, ISO>"}`
- "Approve the two TikTok videos from Jordan" → `submissions_list` with `query {"status": "pending"}`, pick Jordan's, then `submissions_update` each with its version.
