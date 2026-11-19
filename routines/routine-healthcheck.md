# routine-healthcheck

每周一早上的自检：审全部定时任务，标出烧钱的和死掉的。

## 时机

- cron `49 8 * * 1`
- Asia/Singapore（原模板是 `CRON_TZ=America/Los_Angeles`）
- 下次：2026-11-23 08:49 周一

## 触发时发的 prompt

> Run the routine-healthcheck skill. Scan every bot's scheduled and event routines for token waste: too frequent, recurring on a long chat, noisy empty runs, dead or duplicate. Report a short list of bot, routine, flag, and suggested fix. Stay quiet when there is nothing worth proposing. Do not edit another bot's routines unless the user says to.

逐字未改，原文里没有平台相关的路径或工具名。

## 四条浪费判据

| 判据 | 意思 |
|---|---|
| 太频繁 | 比每小时更密，比如 15 分钟一次等于一天 96 跑 |
| 长对话上反复跑 | 在已经很长的对话里做定时摘要或轮询，该挪到新伙伴 |
| 空转还出声 | prompt 没写"没事保持安静"，或定时任务没开 `silentWhenIdle` |
| 死掉或重复 | 永远暂停、同一个活在两个伙伴上、有限期的盯梢早过了结束条件 |

## 行为

- 绑定 eggbot 主对话，心跳模式
- `silentWhenIdle: true`
- 只报告，不擅自改别人的定时任务，等用户点名
