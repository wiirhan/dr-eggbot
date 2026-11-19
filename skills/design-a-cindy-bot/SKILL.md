---
name: "design-a-cindy-bot"
description: "Use this when designing or creating a new Cindy Bot. Ask a few preference questions, write a tight persona, create_teammate, then verify against the live profile."
metadata:
  displayName: "design-a-cindy-bot"
  updatedAt: "2026-11-19T07:00:46.081Z"
---

# Design a Cindy Bot

Create the bot. Do not ship a shareable template unless the user asked for one.

## Data shape

A bot is four fields, in this order:

1. One job. One sentence. What it does every time it wakes.
2. Anti-jobs. What it never does, even if asked. Adjacent work goes to a different bot.
3. Voice. A few words. Match the user, or a named character. Not a generic assistant.
4. Wake. On-demand chat, a standing routine, or both. Quiet when there is nothing to report.

The name is short. `description` is one sentence for the job. `identity_source` carries all four. Do not pad it with leftover tools, model essays, or "I can also help with".

create_teammate takes `name` (required), `description` (one-line job, max 4,000 chars), and `identity_source` (full persona, max 12,000 chars; ignore the legacy `welcome_message` field). That `identity_source` is the whole persona. After create, read the new bot's live profile and compare it to what you intended. Do not trust the tool ack alone.

There is no delete tool. Create only when the job is real.

## Intake

If the person has a job or goal to automate rather than a finished bot spec, run automate-anything first: find the goal, capture the process and its judgment calls, then set up feedback and a trigger. Its plan becomes `identity_source` (with the one-line goal as `description`). Skip it when the job, rules, and wake are already clear.

Ask only preference questions no experiment can settle. Skip any already answered:

- the one job
- voice and name, if they care
- standing routine or on-demand
- who it talks to: this user, other bots, an outside channel

Do not ask for tools, plugins, or model if you can copy a working sibling bot. Do not ask "should I create it?" after the job is clear. If a detail is reversible, like a color or nickname, pick it and say what you picked.

## Coding bots

The bar is pstack, if installed. Read its poteto-mode skill when writing the persona. Bake into `identity_source`:

- one job and anti-jobs
- short, unslopped replies
- repo work goes to a local agent in its own checkout, not the coordinator's
- eng orchestrators spawn a local agent for any eng work, including investigation and quick answers, and never dig the repo themselves
- bug reports get reproduced first with the matching verification skill, and fixed only after a confirmed repro
- the user's default model, if they named one
- pstack and poteto-mode as situational tools, not standing instructions

Do not paste the full pstack playbook into `identity_source`. If pstack is not installed, say so and keep the same tightness anyway.

## Non-coding bots

Same tightness, different job: scout, shopkeep, life admin, dispatcher, writer. Bake into `identity_source`:

- the ONLY job, named in the first sentence
- stay quiet when there is nothing to report
- never do the adjacent verb: a scout does not post, a drafter does not send
- the concrete how: which API, which inbox, which channel

## Authoring skills

When writing or rewriting a shared skill, use poteto-mode if pstack is installed. Keep steps generic. Put bot names and ids in the profile or routine, not the skill. Save with save_teammate_skill.

## After create

Read the live profile back. Tell the user the name and the one-job line. They can delete the bot from the sidebar if they dislike it.

You cannot write another bot's routines. If the job needs a standing routine, message the new bot with the exact routine name, prompt, and schedule or trigger, and tell it to create it. Confirm to the user that you sent it. If the message fails, give them the one-line instruction to paste into that bot.
