---
name: studio-video
description: Use when the user wants an original short video made from a topic or a saved format (faceless explainer, list video, story, chat video, subtitle clip, motion card) and wants to approve the script, frames and clips along the way before it is published. Drives the TrendGuru Studio stage by stage with the user in the loop.
license: MIT
---

# Studio Video, Reviewed Stage by Stage

## Overview

The TrendGuru Studio writes the material and the script, draws the frames, animates the clips, records the voice and assembles the final vertical video. In step mode it stops after every stage so the user approves it or says what to change, right in the chat. A video the user likes becomes a format for more like it.

## Tools

TrendGuru MCP server: `list_formats`, `create_generation`, `wait_generation`, `review_stage`, `create_media_upload`, `approve_generation`, `publish_generation`, `make_format`, `list_accounts`. Paid plans.

## Workflow

1. **Format.** `list_formats` shows saved and built-in formats. Use `formatId` when one fits; otherwise pass `generator` (`video`, `chat-video`, `motion-card`, `subtitle-clip`) and the topic.
2. **Price.** `create_generation` with `dryRun: true`, the `topic`, `language` and any `values` (for example `{ "seconds": 30 }`). Show the credit estimate.
3. **Start after the user agrees.** Same call without `dryRun`, `reviewMode: "step"`, and a `maxCredits` cap the user accepts.
4. **Review loop.**
   - `wait_generation` (up to 50 seconds per call) until `awaiting` names a stage.
   - Show that stage: material or script text, frame and clip links, the `dashboardUrl`. Interactive clients show the widget.
   - Ask the user: approve, or what to change.
   - `review_stage` with `accept`, `redo` plus the user's feedback, `edit` with their edited text, `restore` to an earlier version, or `replace` with their own picture or clip (`create_media_upload` first).
   - Repeat until the final video is ready.
5. **Approve and publish.** `approve_generation`, ask which accounts, then `publish_generation` with `accountIds` and `publishAt`.
6. **Keep the recipe.** If the user likes the result, `make_format` saves it for the next videos.

## Special answers

- `likeness_unsupported`: say at once that branded characters are not drawn and offer recognisable look-alike types (repeat with `lookalikes: true`) or the user's own pictures at the frames step.
- `song_unsupported` or `request_unsupported`: change the topic, or pass `anyway: true` only when the check misread a harmless topic and the user agreed.

## Rules

- Never accept a stage on the user's behalf.
- Redo spends credits again: say so before redoing paid stages.
- `reviewMode: "auto"` only when the user explicitly wants the video without stops.
