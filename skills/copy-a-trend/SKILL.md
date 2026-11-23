---
name: copy-a-trend
description: Use when the user wants their own version of a trending TikTok or YouTube Short, asks to "copy this trend", "make a video like this one", remake a viral format on their topic or in another language, then publish it. Runs TrendGuru AI copy end to end with a price confirmed by the user and a hard credit cap.
license: MIT
---

# Copy a Trend

## Overview

TrendGuru's Studio remakes a trending video as a new original video in the same format: new scenes, new voice, the user's topic and language. A recorded chat becomes a chat video, a meme clip can stay on top of the new scenes. The user approves the price once, the Studio makes the video in a few minutes, and it goes out to any connected account.

## Tools

TrendGuru MCP server: `list_trends`, `get_trend_breakdown`, `estimate_trend_copy`, `copy_trend`, `get_generation`, `retry_generation`, `list_accounts`, `create_post`. Paid plans.

## Workflow

1. **Pick the video.**
   - The user gave a video from the radar: use its id.
   - Otherwise call `list_trends` with `autoCopy: true` and show the top picks with their lift and hook.
2. **Check fit.** `get_trend_breakdown` shows `autoCopy.fit` and the reasons. Tell the user in one line what the Studio will keep (format, pacing, hook structure) and what becomes theirs (topic, voice, scenes).
3. **Price.** Call `estimate_trend_copy` with `videoId`, `language` and the user's `topic` (omit `topic` to let the Studio pick one that fits the format). Show the credit range to the user.
4. **Start only after the user agrees.** Call `copy_trend` with `maxCredits` at least the `to` of the estimate. Only what is used gets charged.
5. **Follow.** Call `get_generation` every 30-60 seconds until `ready` or `failed`.
   - `failed` because the cap ran out: ask the user for a higher cap, then `retry_generation` with the new `maxCredits`. Finished parts are kept and never paid twice.
   - Any other failure: `retry_generation` once, then report the reason.
6. **Show the result.** Give the video link and the caption.
7. **Publish.** Ask which accounts, then `create_post` with `mediaUrls` set to the finished file, `publishAt: "now"` or a time the user picks. YouTube needs `title`.

## Rules

- Never call `copy_trend` before the user has seen and accepted the price.
- Never publish without the user naming the accounts.
- Repeating `copy_trend` with the same arguments within 10 minutes returns the same generation; that is safe.
- Use `language` from the list: English, Russian, Spanish, German, French, Portuguese, Italian, Arabic, Japanese, Chinese.
