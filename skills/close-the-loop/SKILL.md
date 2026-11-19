---
name: "close-the-loop"
description: "Use this when a bot's process is agreed and it needs a way to learn how it is doing and a trigger to run without being asked."
metadata:
  displayName: "close-the-loop"
  updatedAt: "2026-11-19T07:38:32.528Z"
---

# Close the loop

A bot improves when it can see the results of its own work. It runs on its own when something starts it. Set up both before building.

## Feedback

1. Ask: "If you did this yourself, where would you find out it went badly?" Common answers: reviews on Google or Yelp, customer email, social posts, coworker messages, refunds, no-shows.
2. Make each source something the bot can read itself, through a connector, its inbox, or its browser.
3. Define what the bot does with feedback: match it to the records for that case, find the step that went wrong, and propose a change to the process. The person approves changes.
4. If the data does not exist, offer to build a small tool that records it. Example: a repair shop logs arrival, first contact, keys handed over, service start, and service end. The wait time then shows where the delay was.
5. Ask what ID links one case across apps: an email address, an order number, a customer ID, a part number. Ask them to use the same ID everywhere. Without a shared ID the bot cannot connect records.

## Trigger

Without a trigger the bot works only when asked, and the person is still the bottleneck.

1. Ask what starts the work today: an email, a chat message, a form, a new review, a time of day or week.
2. Pick one trigger per job. Event triggers suit work that arrives. Schedules suit reviews and reports.
3. Write each as a routine: name, what it does when it fires, and when to stay quiet.
4. Add a recurring feedback check, usually weekly, that reads the feedback sources and proposes process changes.

Done when every feedback source is reachable and each routine has a name, a prompt, and a trigger.
