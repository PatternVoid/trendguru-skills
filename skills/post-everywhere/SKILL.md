---
name: post-everywhere
description: Use when the user wants to publish or schedule a post, video, image or carousel to several social networks at once (Instagram, TikTok, YouTube, Facebook Pages, X, LinkedIn), cross-post a file from their computer, add a first comment, or adapt one caption per network. Validates against every network's rules before anything goes out.
license: MIT
---

# Post Everywhere

## Overview

One TrendGuru call publishes to every connected account: now, at a scheduled time or as a draft. Local files upload once and go to all networks. Validation checks every network's rules (length, media type and count, required title, daily limit) before a single credit is spent.

## Tools

TrendGuru MCP server: `list_accounts`, `list_profiles`, `create_media_upload`, `validate_post`, `create_post`, `get_post`, `retry_post`, `list_posts`, `get_usage`.

## Workflow

1. **Accounts.** `list_accounts`. Match the networks the user named; confirm the list in one line when it is ambiguous.
2. **Media.**
   - Public URL: pass it in `mediaUrls`.
   - Local file: `create_media_upload` with `filename`, `contentType`, exact `size`; PUT the bytes (`curl -T file.mp4 -H "Content-Type: video/mp4" "<upload url>"`); pass the `mediaId` in `mediaIds`.
3. **Text per network.** One `text` for all, plus `textPerAccount` where a network needs its own voice: X short and punchy, LinkedIn longer and professional, Instagram with hashtags at the end, YouTube with a `title`.
4. **Options.** `optionsPerAccount`: `firstComment` for Instagram, YouTube, Facebook and LinkedIn; `privacy` for TikTok; `visibility` for YouTube.
5. **Validate.** `validate_post` with the same arguments and `publishAt`. Fix every issue it reports. An account at the daily limit returns `nextAvailableAt`: schedule at or after it.
6. **Publish.** `create_post` with `publishAt: "now"`, an ISO time, or no `publishAt` for a draft.
7. **Confirm.** `get_post` shows the status per account and the live links. A failed target: `retry_post`.

## Rules

- Publishing to an account is the user's call: never add accounts they did not ask for.
- Each target costs credits when it goes out; X costs more. `get_usage` shows the balance.
- Up to 10 posts per account in 24 hours on every network.
