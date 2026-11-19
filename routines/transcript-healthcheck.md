# transcript-healthcheck

工作日早上的自检：翻伙伴们的对话，找反复卡壳的地方，提改进建议。

## 时机

- cron `44 8 * * 1-5`
- Asia/Singapore（原模板是 `CRON_TZ=America/Los_Angeles`，模板自己写着"问导入者时区"）
- 下次：2026-11-20 08:44 周五

## 触发时发的 prompt

> Run the transcript-healthcheck skill. Window: since the last successful run, or the last 24 hours if unknown. Fan out parallel miners across the bots' conversations using list_agents and get_chat_history. Report friction and proposals tagged skill, bot, or routine. Stay quiet when there is nothing worth proposing. Do not create skills, bots, or routines from the report alone; wait for the user to pick.

相对原文改了一处：

```
- Fan out parallel miners across agent transcripts under
  /home/box/agent-data/agent-transcripts, skipping sand-subagent- folders.
+ Fan out parallel miners across the bots' conversations using
+ list_agents and get_chat_history.
```

那套目录是 Grok 的磁盘布局，本机不存在；Cindy 这边读对话走宿主工具。

## 行为

- 绑定 eggbot 主对话，心跳模式：跑在它自己的上下文里，能用到它的技能
- `silentWhenIdle: true`：没事不出声，不产生未读；失败仍会弹通知
- 只报告，不擅自建技能、伙伴或定时任务，等用户挑
