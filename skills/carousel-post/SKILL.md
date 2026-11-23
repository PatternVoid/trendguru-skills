---
name: carousel-post
description: Use when the user wants an Instagram, LinkedIn, TikTok photo or Facebook carousel, a swipe post, "X facts about", a listicle in slides, or wants to turn a trending video, a breakdown, an article or their notes into a carousel. Makes the slides with AI pictures and laid-out text in the TrendGuru Studio and publishes them.
license: MIT
---

# Carousel Post

## Overview

The TrendGuru Studio writes a cover, one idea per slide and a closing call to action, draws a picture for every slide with the subject kept clear of the text, lays out the slides in 4:5 (or the format the user picks) and writes the caption with two alternatives. A 7-slide carousel is ready in about a minute.

## Tools

TrendGuru MCP server: `create_generation` (`generator: "carousel"` or `formatId: "builtin:carousel"`), `wait_generation`, `get_generation`, `retry_generation`, `get_trend_breakdown`, `list_accounts`, `create_post`. Paid plans.

## Workflow

1. **Material.**
   - Topic from the user: use it as is.
   - Trending video: `get_trend_breakdown`, then write the topic from its hook and key points so the carousel carries the same idea in slides.
   - Article, notes or transcript: condense into one line of topic plus the points that must appear.
2. **Slide count.** Cover plus one slide per point plus the closing slide. "5 facts" means 7 slides. Range 3 to 10.
3. **Price.** `create_generation` with `dryRun: true`, `generator: "carousel"`, `topic`, `language`, `values: { "slides": N }`. Show the estimate.
4. **Start after the user agrees.** Same call without `dryRun`, `maxCredits` at least the estimate. Use `reviewMode: "step"` when the user wants to approve the text before pictures are drawn.
5. **Follow.** `wait_generation` until `ready`. Show every slide link and the caption variants.
6. **Publish.** Ask which accounts, then `create_post` with `mediaUrls` set to the slide links in order, the chosen caption, and `publishAt`.

## Rules

- Keep slide text short: a title up to six words and one sentence under it.
- Facts on slides must be true and checkable; the Studio writes them, the agent spots obvious errors before publishing.
- If the generation stops on the credit cap, ask for a higher cap and `retry_generation`: paid pictures are reused.
