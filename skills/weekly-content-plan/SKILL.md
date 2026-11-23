---
name: weekly-content-plan
description: Use when the user wants a content plan or calendar for the week or month, asks what and when to post, wants posts prepared and scheduled in advance, or wants autopilot-style posting across their social accounts. Combines their own best posts with fresh niche trends, then makes and schedules the content with TrendGuru.
license: MIT
---

# Weekly Content Plan

## Overview

A plan built on two kinds of evidence: what already works on the user's accounts and what is taking off right now in their niche. Every slot gets a format, a hook, a network and a time, and each one can be produced in the Studio and scheduled in the same conversation.

## Tools

TrendGuru MCP server: everything used by `performance-review`, `trend-radar-brief`, `copy-a-trend`, `studio-video`, `carousel-post` and `post-everywhere`, plus `get_usage`.

## Workflow

1. **Inputs.** Networks, posts per week per network, language, brand voice, topics to avoid. Use sensible defaults when the user does not say: 5 videos and 2 carousels a week.
2. **What works for them.** Run the `performance-review` steps for the last 30 days and keep the winning formats and posting times.
3. **What works in the niche.** Run the `trend-radar-brief` steps and keep the top clusters, hooks and sounds.
4. **Plan.** Mix about 60% proven formats, 30% fresh trends, 10% experiments. Spread across the week, respect up to 10 posts per account per day.
5. **Budget.** `get_usage` for the balance. Sum the dry-run estimates for every slot that needs the Studio and show the total before making anything.
6. **Produce after the user agrees.** Trend copies through `copy-a-trend`, originals through `studio-video`, slides through `carousel-post`, each within its cap.
7. **Schedule.** `create_post` or `publish_generation` with an ISO `publishAt` per slot; confirm with `list_posts`.

## Output

```markdown
# Content Plan: {week}

| Day | Time | Network | Format | Hook | Source | Status |
|---|---|---|---|---|---|---|
| Mon | 18:00 | TikTok | Faceless list | "..." | trend {link} | scheduled |

Credits: {estimate} of {balance}
```

## Rules

- Show the full plan and its credit total before producing anything.
- Times in the user's time zone; ask once if unknown.
- Every slot links its evidence: the user's past post or the trend it adapts.
