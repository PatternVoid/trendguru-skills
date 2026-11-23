---
name: trend-radar-brief
description: Use when the user wants to know what is taking off in their niche on TikTok or YouTube Shorts, asks for a trend brief, viral formats, hooks to steal, trending sounds or "what should I post this week". Pulls small-account videos that beat their own baseline from the TrendGuru trend radar, reads their AI breakdowns and turns them into content angles.
license: MIT
---

# Trend Radar Brief

## Overview

TrendGuru watches the niches of the workspace around the clock and flags videos from small accounts (up to 100k followers) that suddenly got far more views than the account normally does. A video at 8x its own median on a 20k account is a format that works, caught before big accounts copy it. Every trend in a watched niche comes with an AI breakdown: hook, scenes, why it works, how easy it is to remake.

This skill turns that feed into a brief the user can act on today.

## Tools

TrendGuru MCP server (`https://trend.guru/api/mcp`): `list_trend_niches`, `list_trends`, `get_trend_breakdown`, `list_trend_sounds`. Trend tools come with the paid plans.

## Workflow

1. **Niches.** Call `list_trend_niches`. If the user names a topic, pick the matching niche id; otherwise cover every niche.
2. **Trends.** Call `list_trends` with `sort: "score"`, `limit: 20`, per niche when there are several. Run it once with `platform: "all"` when the user publishes on both TikTok and YouTube Shorts.
3. **Clean the list.**
   - Drop items with `promoted: true`: their reach was bought, not earned.
   - Prefer `growing: true` for "jump on it now" picks.
   - Rank by `outlierRatio` (views divided by the account median) and `score`, not by raw views.
4. **Breakdowns.** Call `get_trend_breakdown` for the top 5 to 8 videos. Status `queued` means the analysis is still running: ask again a minute later. Read the hook, the scenes, why it works and `autoCopy.fit`.
5. **Sounds.** Call `list_trend_sounds` with `window: "72h"` and keep the sounds used by several trending videos.
6. **Cluster.** Group the videos by repeated mechanics: hook type, format (talking head, faceless slideshow, chat screenshot, POV, list, before/after), emotional trigger, sound.
7. **Angles.** For every cluster write two or three ideas adapted to the user's brand. Say which ones the Studio can make automatically (`autoCopy` true) so the user can go straight to `copy-a-trend`.

## Output

```markdown
# Trend Brief: {niche}, {date}

## Act on these first
| # | Video | Account size | Lift vs own median | Still growing | Why it works | Copy with AI |
|---|---|---:|---:|---|---|---|

## Repeating formats
1. **{format}**: what repeats, 2-3 example links.

## Hooks to adapt
- "{exact hook}" ({link})

## Sounds rising in the niche
| Sound | Trending videos using it | Combined views per hour |
|---|---:|---:|

## Ideas for {brand}
1. {idea}: format, hook, sound, ready for AI copy yes/no
```

## Rules

- Quote hooks exactly as the breakdown gives them and link every video.
- Judge by lift against the account's own median, never by raw views across accounts of different size.
- Keep TikTok and YouTube Shorts apart when comparing numbers.
- End with a clear next step: copy a trend (`copy-a-trend`), make an original video (`studio-video`) or a carousel (`carousel-post`).
