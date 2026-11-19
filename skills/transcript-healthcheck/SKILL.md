---
name: "transcript-healthcheck"
description: "Use when auditing Cindy Bot fleet transcripts for user friction, proposing new skills, bots, or routines from repeated corrections, or running the standing transcript-healthcheck routine."
metadata:
  displayName: "transcript-healthcheck"
  updatedAt: "2026-11-19T07:43:58.614Z"
---

# Transcript healthcheck

Scan Cindy Bot conversations for user friction in a time window. Propose new skills, bots, or routines only when evidence supports them. Do not create anything until the user picks a proposal.

## When to run

- the standing transcript-healthcheck routine fires
- the user asks for a fleet checkup, friction audit, or "what should we automate"

## Window and corpus

The default window is the last 24 hours, unless the routine or the user names another.

The bots come from `list_agents`. It returns each bot's id, its name, and its main chat session id. Read the traffic with `get_chat_history`:

- pass the bot's session id, with `from` and `to` set to the window
- keep the default roles. That returns user, assistant, ask_user and plan_review, and drops tool_use, tool_result and thinking
- page with `nextCursor` until `hasMore` is false
- a session that returns NOT_FOUND is gone. Skip it and do not reconstruct it

State the window and bot count before mining.

## How to mine

Fan out parallel subagents, each with a slice of session ids. Keep only their findings in the main thread. Each returns one block per bot with user traffic in the window: bot name, user goals, friction signals with short quotes, repeated corrections, misunderstandings, and candidate gaps tagged skill, bot, or routine.

Friction to look for: frustration, "stop", "wrong", "i said", "undo", the same instruction restated, the user doing work the bot should own, the bot asking questions an experiment could settle, and abandoned threads.

Skip bots with no user messages in the window.

## Report

Lead with at most 5 bullets. Then a short list of proposals, each tagged skill, bot, or routine, with the evidence that earned it.

Stay quiet when the routine fires and there is nothing to propose.

## Implement, after the user picks

1. Skills: use poteto-mode if pstack is installed, keep the skill generic, and save with save_teammate_skill.
2. Bots: use design-a-cindy-bot.
3. Routines: list the existing ones with `schedule_list`, then change one with `schedule_update`, or add one with `schedule_create`.
