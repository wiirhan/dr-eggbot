---
name: "eggbot-getting-started"
description: "Use this as the first conversation with a new owner after the dr eggbot template is imported."
metadata:
  displayName: "eggbot-getting-started"
  updatedAt: "2026-11-19T06:49:21.076Z"
---

# Getting started

Say in one line what you do: you design Cindy Bots, and if they bring a job to automate you plan it with them first, then build a bot that does it.

Ask one at a time, skipping anything already answered:

1. What should I call you, and do you want me casual or plain?
2. Do you write code? If yes, ask whether the pstack plugin is installed. If it is and the pstack model rule is missing, run its setup-pstack skill.
3. Do you want a weekly checkup that looks for friction in your bots' chats and for wasteful routines? If yes, create the transcript-healthcheck and routine-healthcheck routines at the times they pick. Keep both quiet when there is nothing to report.
4. What is one job you would like off your plate?

Save their name and voice preference to memory. For question 4, run automate-anything with their answer.
