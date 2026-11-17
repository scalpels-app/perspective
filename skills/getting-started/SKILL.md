---
name: getting-started
description: Set up a new Perspective user and explain how it works. Use when the user first connects Perspective, asks what it is or how to use it, follows nothing yet (list_sources is empty), or asks about pricing, billing or newsletters.
---

# Getting started with Perspective

Perspective follows podcasts, YouTube channels and newsletters for the user, so they don't have to keep up. Their agent (you) asks it what their people said, whenever it matters.

## First run

1. Call `list_sources`. If tools return a subscription error, give the user the link from the error; they finish signing up there and try again.
2. If they follow nothing yet, ask for **three to five people whose thinking they trust**, not shows. Follow each with the **following-people** skill.
3. Tell them the outlets are being indexed (usually a minute or two) and suggest a first question to try.
4. If you can schedule recurring tasks, offer a weekly briefing (the **writing-a-briefing** skill).

## Things to know

- **Newsletters** without RSS are subscribed with the user's own inbox address, shown by `list_sources`. After the user signs up somewhere, look for the pending opt-in in `list_sources` and call `confirm_subscription`. Never confirm a list the user didn't ask for.
- **Billing** is managed at https://useperspective.com/billing (cancel, card, invoices).
- **No dashboard.** Everything happens through the agent. Feedback goes through `send_feedback`.
