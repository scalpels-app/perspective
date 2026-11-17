---
name: growing-the-library
description: Widen what the user follows in Perspective over time by noticing the people their sources talk about and offering them at the right moment. Use whenever you read Perspective search results or episodes, when search returns suggest_following, and when the user asks who else to follow.
---

# Growing the library

A Perspective library should get wider over time, so the user hears more than one circle's take. The best new voices come from the people the user already trusts: who they argue with, quote, recommend and interview. Your job is to notice those people and offer them, one at a time, when it's relevant.

## While reading

Whenever you read an item (`get_item`, or a passage in `search` results) and the hosts discuss, quote, recommend, interview or argue with someone who publishes their own work, call `save_lead` quietly. Don't mention it to the user or pause your answer.

- Name the **person**, not their show. Use `kind: show` only when there's no person behind it.
- Write the `reason` as one concrete sentence a user would care about: who said what about them, where. "Aaron and Ian argued with Jason Cohen's pricing advice on Mostly Technical", not "mentioned on a podcast".
- Pass the `item_id`.
- Saving someone again counts another mention; that's how Perspective knows who keeps coming up.
- Skip people who are only name-dropped in passing, and people the user obviously already follows.
- Transcripts mishear names. Before `save_lead`, `record_related` or `find_person`, get the spelling right from the show notes, the episode's links, or what you know; a web search settles it if you're unsure. A misspelled name creates a stranger in the shared map instead of adding to the real person.

Also call `record_related` for the same relationship: `person` is the host or author, `related` is the other person with URLs of what they publish now (only ones you know or found; leave the rest out), plus the `item_id`. This feeds Perspective's shared map of who's in whose conversation, so other users' agents don't have to rediscover it. Send only public facts about the two people, never anything about the user or why it matters to them; that belongs in `save_lead`'s reason.

## Offering

When `search` returns `suggest_following`, finish answering the user's question first. Then offer it in one sentence built from the reason:

> Aaron and Ian had some interesting things to say about Jason Cohen. Want me to add what he publishes?

- If yes, follow them with the **following-people** skill (`find_person`, then `follow` with `person`).
- If no, call `dismiss_lead` so Perspective stops suggesting them.
- If the user ignores it, drop it; Perspective will offer it again another time.

Offer at most one person per answer, and never interrupt an answer to do it.

## When the user asks to grow it

For "who else should I follow?" or "widen my feed", call `list_leads` (people your own reading turned up) and `related_people` without a name (people who've come up recently around everyone the user follows, from the shared map, with where they publish). Offer three to five people, each with a concrete reason. Prefer:

1. people who came up more than once, or recently;
2. people relevant to what the user has been asking about;
3. people who'd add a different view: a critic, a practitioner from another field, someone outside the user's usual circle.

Use `expand_source` on a followed show for more ideas (links in show notes, shows named in transcripts). Treat its results as leads about people, and never suggest a host's dormant shows.
