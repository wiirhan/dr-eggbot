---
name: "routine-healthcheck"
description: "Use when auditing Cindy Bot routines for token waste, deciding cadence, or running the standing routine-healthcheck wake."
metadata:
  displayName: "routine-healthcheck"
  updatedAt: "2026-11-19T07:45:20.012Z"
---

# Routine healthcheck

Scan the fleet's scheduled and event routines for token waste. Report what to change. Do not edit another bot's routines unless the user says to.

## When to run

- the standing routine-healthcheck routine fires
- the user asks for a routine checkup, token audit, or cheaper wakes
- before creating a new standing routine

## How to scan

1. Get the bots and their names with `list_agents`.
2. Call `schedule_list` with `device: "all"` so routines on every computer come back, not just this one. Each row carries the cron, the next and last fire, the status, and the session it is bound to.
3. Note schedule or event trigger, enabled or paused, and whether it stays quiet when nothing changed (`silentWhenIdle`, or a line in the prompt).

## Flags

Call out each hit with the bot name, routine name, and one fix line.

- Too frequent. A cron denser than hourly, for example every 15 minutes, which is about 96 runs a day. Prefer hourly or a few times a day. Prefer an event listener when the trigger is Slack, GitHub, or similar.
- Recurring on a long chat. A standing digest or poll on a bot whose transcript is already long. Move that job to a fresh bot.
- Noisy empty runs. The prompt never says to stay quiet when nothing changed. Add that. On a schedule, set `silentWhenIdle`.
- Dead or duplicate. Paused forever, the same job on two bots, or a finite watch past its end condition.

## Report

One short list: bot, routine, flag, suggested fix. Offer to apply fixes only after the user picks which ones.
