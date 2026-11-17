---
name: writing-a-briefing
description: Write a Perspective content briefing of what the user would most want to know from what they follow, and set it up to run on a schedule. Use when the user asks "what did I miss?", for a digest, catch-up or briefing, when running as a scheduled Perspective task, or after setup when offering a weekly briefing.
---

# Writing a briefing

A briefing is not a list of everything new. It's a short note with what the user would most want to know from the people they follow right now. Most weeks it should take two minutes to read.

You decide what that is. Use everything you know about the user: what they've been working on, building, deciding or worrying about, from this conversation, your memory, their projects and recent sessions you can see. That picture is your main guide. Perspective's search history fills in what you can't see.

## Gather

1. Call `get_briefing`. It returns:
   - `new_items`: everything published in their library since the last briefing.
   - `recent_topics`: what the user asked Perspective about in the last two weeks. Every topic they asked about more than once, or very recently, deserves a look: they asked for a reason. Treat the rest as hints, not a checklist.
   - `recently_followed_people`, `top_leads`, and `related_to_your_people` (who has come up recently around the people they follow).
   Calling it marks the briefing as done, so call it once per briefing.
2. Decide on three to five themes the user would most likely care about this week. Combine what you know of their work and life with `recent_topics`, and let `new_items` surprise you: a cluster of new episodes on something close to their work counts even if they never searched for it.

## Cover those themes first

For each theme:

- `search` the topic with synonyms and `since_days` covering the briefing window.
- `get_item` on the best one or two hits and read the relevant part.
- Note who said what, with a link to the moment (`jump_url`, or `&t=<seconds>s`).

Skip a theme when nothing new touches it. Don't pad, and don't explain how you chose themes.

## Then highlights

Scan `new_items` for two or three things worth knowing even though the user didn't ask: a strong take, a notable guest, a show covering something unusual for it, several of their people on the same subject the same week. Read before recommending; titles mislead.

## Enrich as you read

This is the best time to grow the library. Follow the **growing-the-library** skill: whenever an episode features a guest, or the hosts discuss or quote someone who publishes their own work, call `save_lead` with a specific reason and `record_related` with the public facts. Guests count.

## Write it

- **On your mind:** one short paragraph per theme: who said what, when, linked. Name the person, then the show.
- **Also worth your time:** two or three highlights, one or two sentences each, linked.
- **Someone to add:** at most one person from `top_leads`, `related_to_your_people` or what you just read, with the reason, as a question ("Want me to add what Jason Cohen publishes?").

Keep it under about 300 words. No item-by-item list of new episodes. If almost nothing new touches their themes, say so in a line and keep the highlights.

## Scheduling

If your harness can run tasks on a schedule (scheduled tasks, routines, automations), offer once to set up a recurring briefing, weekly by default, at a time the user picks. The scheduled prompt should be short, for example: "Use the Perspective writing-a-briefing skill to write my briefing." Deliver it however the harness delivers scheduled results.

If you can't schedule, offer the briefing on demand instead ("ask me 'what did I miss?' any time").

In a scheduled run nobody is there to answer questions. Don't follow anyone or dismiss leads on your own; put the suggestion in the briefing for the user to answer later.
