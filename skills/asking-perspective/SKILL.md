---
name: asking-perspective
description: Answer "what are my people saying about X?" from the podcasts, videos and newsletters the user follows in Perspective. Use when the user asks what their sources, follows or "people" think about a topic, or asks about something those people may have covered recently.
---

# Asking Perspective

The user wants to know what the specific people they follow have said, with links, so they can trust it and jump to it. They don't want a general answer from you.

## Steps

1. **Search broadly.** Call `search` with the topic plus synonyms and the phrasings a host would actually say out loud. It's keyword search, so breadth matters: `saas "build vs buy" "in-house" "vibe coding" replace subscriptions internal tools`. Add `since_days` when the user means recent.
2. **Read the best hits.** Call `get_item` on the two or three strongest results and read the relevant part. Page with `offset` for long transcripts.
3. **Fill gaps.** A YouTube hit marked `transcript_missing` matched only on its title. If it looks relevant, call `transcribe_video`. It may give you a command to run on the user's computer; run it, then search again.
4. **Answer.** Lead with who said what and when. Give each claim its link: use `jump_url` from search, or the video URL with `&t=<seconds>s` from the `[m:ss]` markers in `get_item`. Keep it short; offer to pull more detail.
5. **Say when there's nothing.** If the user's people haven't covered it, say so plainly. Don't fill in with your own view unless they ask. Suggest following someone who would cover it.

While reading, follow the **growing-the-library** skill: save the people the hosts talk about, and offer `suggest_following` after your answer.

## Feedback

If the user is frustrated with Perspective, or wishes it did something, offer to pass that on and call `send_feedback` with their words and what they were doing.
