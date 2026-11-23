---
name: performance-review
description: Use when the user asks how their social accounts are doing, which posts worked, why a post took off, what to post more of, or wants a weekly or monthly report on Instagram, TikTok, YouTube, Facebook, X or LinkedIn. Finds the user's own outlier posts against their median and turns them into next steps.
license: MIT
---

# Performance Review

## Overview

TrendGuru syncs analytics of every connected account, including posts made outside TrendGuru. This skill compares each post with the account's own median, finds the winners, explains what they share and says what to make next.

## Tools

TrendGuru MCP server: `list_accounts`, `get_account_analytics`, `get_top_posts`, `list_posts`, `get_post`.

## Workflow

1. **Window.** Default 30 days; use what the user asks.
2. **Accounts.** `get_account_analytics` with `days`: followers and their change, posts, engagement against the previous period, engagement rate, reach and watch time where the network gives them.
3. **Posts.** `get_top_posts` per account with `days`, `limit: 50`, `sortBy: "recent"` to get a fair sample, then again with `sortBy` set to the main metric (`views` for video networks; `likes` or `comments` for X and LinkedIn; `saves` for Instagram carousels).
4. **Baseline.** Per account and per format, take the median of the main metric. Lift = post metric / median.
   - 5x and more: breakout
   - 2x to 5x: strong
   - 1.5x to 2x: above normal
5. **Explain the winners.** Compare their hook, format, topic, length, posting time and caption with the rest. Name what repeats.
6. **Next steps.** Three to five concrete posts to make next, each tied to the evidence.

## Output

```markdown
# Performance Review: {accounts}, last {N} days

## Headline numbers
| Account | Followers | Change | Posts | Engagement rate | vs previous period |
|---|---:|---:|---:|---:|---:|

## Breakout posts
| Post | Account | Metric | Lift vs median | What made it work |
|---|---|---:|---:|---|

## What repeats in the winners
1. ...

## Make next
1. {post idea}: why, format, best time
```

## Rules

- Lift against the account's own median, never raw numbers across accounts of different size.
- Separate networks and formats when computing the median.
- Link every post.
- For fresh ideas from outside the account, follow with `trend-radar-brief`.
