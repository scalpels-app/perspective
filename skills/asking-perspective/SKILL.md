---
name: asking-perspective
description: Answer "what are my people saying about X?" from the podcasts, videos and newsletters the user follows in Perspective. Use when the user asks what their sources, follows or "people" think about a topic, or asks about something those people may have covered recently.
---

# Asking Perspective

The user wants to know what the specific people they follow have said, with links, so they can trust it and jump to it. They don't want a general answer from you.

## Steps

1. **Search broadly.** Call `search` with the topic plus synonyms and the phrasings a host would actually say out loud. It's keyword search, so breadth matters: `saas "build vs buy" "in-house" "vibe coding" replace subscriptions internal tools`. Add `since_days` when the user means recent.
   - **Names are often misspelled.** Most transcripts are machine-made (Whisper or YouTube's automatic captions), and they mishear names: "Laravel" becomes "level", "LaraJobs" becomes "layer jobs" or "LairJobs", "Svix" becomes "Zvix". Search matches words, not sounds, so when the question hinges on a person, company or product, put three kinds of terms in one search: the name, its likely mishearings (sound-alike spellings, and split or merged forms like `"lara jobs"`), and the words that would surround it (their company, product, co-host, the topic). Show notes are written by the publisher and spelled right, so the episode often matches on them even when the transcript doesn't.
   - An empty result for a name alone doesn't mean nobody mentioned it. Try the surrounding topic before telling the user nobody did.
2. **Read the best hits.** Call `get_item` on the two or three strongest results and read the relevant part. Page with `offset` for long transcripts.
3. **Fill gaps.** A YouTube hit marked `transcript_missing` matched only on its title. If it looks relevant, call `transcribe_video`: Perspective fetches the captions, or queues them when YouTube blocks it (they usually arrive within half an hour). Search again once they're in, and tell the user that video wasn't covered yet if you answer before then.
4. **Answer.** Lead with who said what and when. Give each claim its link: use `jump_url` from search, or the video URL with `&t=<seconds>s` from the `[m:ss]` markers in `get_item`. When you quote, fix names the transcript obviously misheard (you know it's "Laravel", not "level"); this is a transcription error, not the speaker's. Keep it short; offer to pull more detail.
5. **Look outside their network when it helps.** `search` also returns `out_of_network`: a few matches from sources the user doesn't follow. These are link-only citations: you can't `get_item` them, so cite the title and link and don't present more than the snippet. Lead with the user's own sources. Cite out-of-network ones when the question reaches beyond their people ("is anyone making a case for…?") or when their own sources are thin, and offer to follow the person behind a useful one (`find_person`). While Perspective is young this list is often empty; then use your own web search if the user wants a wider answer.
6. **Say when there's nothing.** If nobody in Perspective has covered it, say so plainly. Don't fill in with your own view unless they ask. Suggest following someone who would cover it.

While reading, follow the **growing-the-library** skill: save the people the hosts talk about, and offer `suggest_following` after your answer.

## Feedback

If the user is frustrated with Perspective, or wishes it did something, offer to pass that on and call `send_feedback` with their words and what they were doing.
