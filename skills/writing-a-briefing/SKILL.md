---
name: writing-a-briefing
description: Write a Perspective content briefing focused on what the user has been thinking about, and set it up to run on a schedule. Use when the user asks "what did I miss?", for a digest, catch-up or briefing, when running as a scheduled Perspective task, or after setup when offering a weekly briefing.
---

# Writing a briefing

A briefing is not a list of everything new. It's a short note that tells the user what their people said about the things on their mind, plus a few things worth knowing about anyway. Most weeks it should take two minutes to read.

## Gather

1. Call `get_briefing`. It returns:
   - `recent_topics`: what the user searched for in the last two weeks. This is the best evidence of what they're thinking about.
   - `new_items`: everything published in their library since the last briefing.
   - `recently_followed_people` and `top_leads`.
   Calling it marks the briefing as done, so call it once per briefing.
2. Add what you know about the user's current interests from this conversation, your memory, or recent sessions you can see. Treat these the same as `recent_topics`.

## Focus on their topics first

For each of the three to five strongest topics (most recent, asked most often, or clearly ongoing):

- `search` the topic with synonyms and `since_days` covering the briefing window.
- `get_item` on the best one or two hits and read the relevant part.
- Note who said what, with a link to the moment (`jump_url`, or `&t=<seconds>s`).

Skip a topic when nothing new touches it. Don't pad.

## Then highlights

Scan `new_items` for two or three things worth knowing even though the user didn't ask: a strong take, a notable guest, a show covering something unusual for it, several of their people on the same subject the same week. Read before recommending; titles mislead.

## Enrich as you read

This is the best time to grow the library. Follow the **growing-the-library** skill: whenever an episode features a guest, or the hosts discuss or quote someone who publishes their own work, call `save_lead` with a specific reason. Guests count.

## Write it

- **On your mind:** one short paragraph per topic: who said what, when, linked. Name the person, then the show.
- **Also worth your time:** two or three highlights, one or two sentences each, linked.
- **Someone to add:** at most one person from `top_leads` or from what you just read, with the reason, as a question ("Want me to add what Jason Cohen publishes?").

Keep it under about 300 words. No item-by-item list of new episodes. If almost nothing new touches their topics, say so in a line and keep the highlights.

## Scheduling

If your harness can run tasks on a schedule (scheduled tasks, routines, automations), offer once to set up a recurring briefing, weekly by default, at a time the user picks. The scheduled prompt should be short, for example: "Use the Perspective writing-a-briefing skill to write my briefing." Deliver it however the harness delivers scheduled results.

If you can't schedule, offer the briefing on demand instead ("ask me 'what did I miss?' any time").

In a scheduled run nobody is there to answer questions. Don't follow anyone or dismiss leads on your own; put the suggestion in the briefing for the user to answer later.
