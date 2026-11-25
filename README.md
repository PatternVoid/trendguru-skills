# TrendGuru Skills for AI Agents

Ready-made social media workflows for Claude Code, Claude, Cursor, Codex and every agent that supports the [Agent Skills](https://agentskills.io) format, powered by the [TrendGuru MCP server](https://trend.guru/mcp).

Your agent finds what is taking off in your niche, remakes it as your own video or carousel, shows you every stage for approval and publishes to Instagram, TikTok, YouTube, Facebook, X and LinkedIn in one call.

## Install

Claude Code plugin (skills and the MCP server in one step):

```bash
/plugin marketplace add PatternVoid/TrendGuru-Skills
/plugin install trendguru@trendguru
```

Any agent with Agent Skills support:

```bash
npx skills add PatternVoid/TrendGuru-Skills
```

Then connect the MCP server if your agent does not have it yet:

```bash
claude mcp add --transport http trendguru https://trend.guru/api/mcp
```

The first call opens TrendGuru sign-in: pick a workspace and allow access. An API key works too: add `--header "Authorization: Bearer tg_live_..."`. Keys live in the dashboard under API keys.

## Skills

| Skill | Ask your agent | You get |
|---|---|---|
| [`trend-radar-brief`](skills/trend-radar-brief/) | "What is taking off in my niche this week?" | Videos from small accounts that beat their own median, hooks, formats, rising sounds, ideas for your brand |
| [`copy-a-trend`](skills/copy-a-trend/) | "Make my own version of this trend in Spanish" | A new original video in the same format, made within a credit cap you approve, ready to publish |
| [`studio-video`](skills/studio-video/) | "Make a 30-second faceless video about compound interest" | Script, frames, clips and voice, each shown to you for approval, then the final video |
| [`carousel-post`](skills/carousel-post/) | "Turn this trend into a 7-slide Instagram carousel" | Slides with AI pictures and laid-out text plus three caption options |
| [`post-everywhere`](skills/post-everywhere/) | "Post this video to TikTok, Reels and Shorts tomorrow at 6 pm" | One validated post to every network, with a caption tuned per network |
| [`performance-review`](skills/performance-review/) | "Which of my posts worked this month and why?" | Your breakout posts against your own median and what to make next |
| [`weekly-content-plan`](skills/weekly-content-plan/) | "Plan and schedule next week" | A calendar built on your winners and fresh trends, produced and scheduled |

## How it works

```text
TrendGuru MCP server (https://trend.guru/api/mcp)
        │
        ├─ trend radar ── trend-radar-brief ── copy-a-trend
        ├─ Studio ─────── studio-video, carousel-post
        ├─ publishing ─── post-everywhere
        └─ analytics ──── performance-review
                                 └── weekly-content-plan ties them together
```

Every paid step goes through a price check first: the agent shows the estimate, you agree, and the run stays inside the cap you set. Publishing always goes to the accounts you name.

## Links

- [TrendGuru](https://trend.guru)
- [MCP server](https://trend.guru/mcp)
- [Publishing API](https://trend.guru/api)
- [Docs](https://trend.guru/docs)
- [OpenAPI](https://trend.guru/openapi.json)

MIT License.
