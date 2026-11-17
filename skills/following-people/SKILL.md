---
name: following-people
description: Follow a person in Perspective by finding everything they publish now. Use when the user names someone to follow ("follow Aaron Francis", "add Jason Cohen", "I like what Lenny says"), or names a show when what they really want is its host.
---

# Following people

Perspective users follow people, not shows. The user should be able to say a name and trust you to find where that person is talking right now. Don't ask them to name podcasts, channels or newsletters.

## Steps

1. **Find their outlets.** Call `find_person` with the name. It returns podcasts they host and YouTube channels under their name, split into `active` (published in the last few months) and `dormant`. It also includes outlets Perspective's map knows for them that the directories don't list. Directory searches are reused for up to two weeks, so pass `refresh: true` when the user says they started something new or the list looks incomplete.
2. **Drop strangers.** Same-name results are common: "Pastor Aaron Francis" hosts a church podcast. Keep a result only if its genres, description or title fit what you know about the person. If you can't tell which person the user means, ask one short question ("Jason Cohen the WP Engine founder?").
3. **Look for writing.** Newsletters and blogs aren't in the directories. Search the web for the person's newsletter, Substack or blog. Prefer anything with an RSS feed (Substack: the publication URL works).
4. **Follow the active outlets.** Call `follow` with the URLs from step 1 and 3, and set `person` to their name. Follow everything active that is really theirs; the user asked for the person, not one show.
5. **Report briefly.** Say what you followed in one or two lines. Mention dormant shows only in passing ("Get Out of My Head hasn't had an episode since 2020, so I skipped it"). Never follow a dormant show unless the user insists.

## Edge cases

- **The user names a show.** Follow the show. If it has clear hosts, offer to follow them as people too ("Want me to follow Aaron and Ian everywhere they publish?").
- **Newsletters without RSS.** The user subscribes with their Perspective inbox address (`list_sources` shows it). After they do, check `list_sources` for a pending opt-in and call `confirm_subscription`. Never confirm a list the user didn't ask for.
- **Mostly a guest.** Some people rarely host anything; they show up on other people's shows. Say so, follow what they do publish, and save them with `save_lead` so their appearances keep surfacing.
- **Nothing found.** Tell the user plainly and suggest they paste a link if they know one.
