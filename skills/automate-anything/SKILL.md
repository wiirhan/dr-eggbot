---
name: "automate-anything"
description: "Use this when someone wants to automate a job, hand work to a bot, or build a bot for a goal. Runs the full flow from goal to a working bot with a trigger."
metadata:
  displayName: "automate-anything"
  updatedAt: "2026-11-19T07:03:29.755Z"
---

# Automate anything

Automation is a goal plus a process, with a bot doing the process. This skill turns one person's job into one bot that does it without them.

Run the stages in order. Each stage ends in something the person confirms. Do not skip ahead to building.

| Stage | Skill | Done when |
|---|---|---|
| 1. Goal | find-the-goal | The person agrees to a one-line goal that names an outcome, not a step |
| 2. Process | capture-the-process | The person says the played-back process and its judgment calls are right |
| 3. Loop | close-the-loop | The bot has a feedback source and a trigger |
| 4. Build | design-a-cindy-bot, or create_teammate | The bot exists and its live profile matches the plan |

## Rules

- One question per message. Short messages. Plain words, no jargon.
- Assume the person is not technical. When they doubt a bot can do a step, say what the bot would actually do: click through the site, read the inbox, join the call, write a small script.
- The goal outranks the process. If a step does not serve the goal, say so and offer to drop it. If the person wants their exact process kept, keep it.
- Do not execute the job during stages 1 to 3. Planning only.
- Keep a running plan in your own notes: goal, steps, judgment calls, sources, feedback, trigger. Play the whole thing back once before stage 4.
- If the person already answered a stage elsewhere in the chat, play it back and confirm instead of asking again.

## Build

Put the one-line goal in `description`. The new bot's `identity_source` carries:

1. The goal, as its one job, in the first sentence.
2. The process as short steps.
3. The judgment calls as rules, including which source wins and what done means.
4. When to ask the person instead of deciding.
5. The feedback check and what to do with it.
6. Anti-jobs: adjacent work it never does.

The routine from stage 3 is created by the new bot itself. Message the new bot with the exact routine name, prompt, and schedule or trigger. Then tell the person which apps to connect first.

After building, offer one review: check the process against the goal and suggest a simpler way, if there is one.
