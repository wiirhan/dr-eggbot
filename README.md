# dr eggbot

Cindy 伙伴 **dr eggbot** 的完整快照：说明、技能、定时任务。

它只干一件事：把一件想从手上卸掉的活，变成一个能自己跑的伙伴。

## 来源

照着 X 上 [@poteto](https://x.com/poteto)（Lauren Tan，Cursor）发布的 Grok Bot 模板 **dr eggbot v2** 移植过来：

- 原帖：https://x.com/poteto/status/2123159763626430464
- 市场页：https://x.ai/bot/marketplace/bots/dr-eggbot-v2

技能正文主体按原模板保留，主要做了以下几类平台适配改动：

| 原文 | 改后 | 原因 |
|---|---|---|
| `Grok Bot` / `Grok Bots`、`design-a-grok-bot` | `Cindy Bot` / `Cindy Bots`、`design-a-cindy-bot` | 换平台 |
| `CreateAgent`（单 `description`）/ `UpdateSkill` / `UpdateRoutine` 等 | `create_teammate`（`name` + `description` + `identity_source`）/ `save_teammate_skill` / `schedule_list` / `schedule_update` / `schedule_create` | Cindy 的工具名与入参 |
| `/home/box/agent-data/...` 磁盘路径、`cloud agent` | `list_agents` + `get_chat_history`、`schedule_list`、`silentWhenIdle`、`local agent` | 本机没有那些目录，也没有云 agent，改走宿主工具 |

## 目录

```
dr-eggbot/
├── bot/
│   ├── SOUL.md          它的人格与设计标准
│   └── README.md        运行配置说明、创建时用的入参
├── skills/              8 个技能（<name>/SKILL.md，导入 Cindy 后位于 .agents/skills/）
└── routines/            2 个定时任务的说明
```

## 八个技能

| 技能 | 干什么 |
|---|---|
| [`eggbot-getting-started`](skills/eggbot-getting-started/SKILL.md) | 第一次见面：问称呼、口吻、写不写代码、要不要自检、想卸掉哪件活 |
| [`automate-anything`](skills/automate-anything/SKILL.md) | 四阶段访谈，把一件活变成一份 bot 说明 |
| [`find-the-goal`](skills/find-the-goal/SKILL.md) | 第 1 阶段：把"步骤"挤成"结果" |
| [`capture-the-process`](skills/capture-the-process/SKILL.md) | 第 2 阶段：脑倒 → 复述 → 判断点 → 更好的做法 |
| [`close-the-loop`](skills/close-the-loop/SKILL.md) | 第 3 阶段：反馈来源 + 触发 |
| [`design-a-cindy-bot`](skills/design-a-cindy-bot/SKILL.md) | 第 4 阶段：四字段写 persona，建完读回校验 |
| [`transcript-healthcheck`](skills/transcript-healthcheck/SKILL.md) | 扫伙伴们的对话，找反复卡壳的地方 |
| [`routine-healthcheck`](skills/routine-healthcheck/SKILL.md) | 审定时任务有没有白烧钱 |

## 两个定时任务

| 名称 | cron | 时区 | 频率 |
|---|---|---|---|
| [`transcript-healthcheck`](routines/transcript-healthcheck.md) | `44 8 * * 1-5` | Asia/Singapore | 工作日 08:44 |
| [`routine-healthcheck`](routines/routine-healthcheck.md) | `49 8 * * 1` | Asia/Singapore | 周一 08:49 |

两个都绑定在 eggbot 的主对话上（心跳模式），`silentWhenIdle: true`：没事不出声，失败仍会通知。

原模板是 08:44 / 08:49 洛杉矶时间，并按模板要求问了导入者时区，这里选的是本机时区。

## 怎么用

这份不是能直接装的东西，是档案。要重建：

1. 用 [`bot/SOUL.md`](bot/SOUL.md) 作 `identity_source` 调 `create_teammate`，`name`、`description` 和运行配置（需 `mcpMode: inherit`，否则两个自检技能拿不到宿主工具）见 [`bot/README.md`](bot/README.md)
2. 把 `skills/*/SKILL.md` 逐个 `save_teammate_skill`
3. 按 [`routines/`](routines/) 下每份说明里的 cron、时区、prompt 调 `schedule_create`，绑定到 eggbot 主对话并开启 `silentWhenIdle: true`

要改行为，改 Cindy 里伙伴自己的那份，再把这里同步过来。这里不会自动跟着变。
