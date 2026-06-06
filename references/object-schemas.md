# Feishu Object Schemas

## Naming

Use this default naming pattern:

```text
<项目名> - 项目总览
<项目名> - 项目管理
```

Reuse existing objects with the same names when possible.

`<项目名> - 项目管理` is one Feishu Base app. Create the tables below inside it instead of creating five separate Base files.

Do not create `<项目名> - 项目全景白板 brief` as a default document. A whiteboard brief should normally stay in the agent reply and be handed to `beautiful-feishu-whiteboard` when that skill is available. Create a brief document only if the user explicitly asks to persist the prompt.

## Project Overview Doc

Sections:

```text
背景
目标
当前状态
关键资料
核心判断
待确认事项
下一步行动
关联链接
```

## Source Index Table

| Field | Type | Notes |
| --- | --- | --- |
| 标题 | text | Source title or file name |
| 类型 | select | feedback, interview, PRD, meeting, competitor, chat, task, decision |
| 来源 | text | File path or Feishu link |
| 摘要 | text | Short source summary |
| 关联对象 | text | Related requirement, task, risk, or doc |
| 更新时间 | date | Last processed date |

## Requirement Pool Table

| Field | Type | Notes |
| --- | --- | --- |
| 需求 | text | User or business need |
| 来源 | text | Evidence source |
| 用户证据 | text | Quote, observation, or artifact |
| 影响范围 | select | 用户, 业务, 技术, 运营, 待确认 |
| 优先级 | select | P0, P1, P2, P3, needs confirmation |
| 状态 | select | new, reviewing, accepted, parked, rejected |
| 关联资料 | text | Source index or doc link |

## Competitor Matrix Table

| Field | Type |
| --- | --- |
| 竞品 | text |
| 定位 | text |
| 功能 | text |
| 定价 | text |
| 差异点 | text |
| 启发 | text |
| 风险 | text |

## Task Plan Table

| Field | Type | Notes |
| --- | --- | --- |
| 任务 | text | Actionable task |
| 模块 | text | Product or workstream module |
| 负责人 | text | Owner if known |
| 优先级 | select | P0, P1, P2, P3 |
| 预估工时 | text | Estimate |
| 开始日期 | date | Optional |
| 截止日期 | date | Optional |
| 状态 | select | todo, doing, blocked, done |

## Risk And Decision Log Table

| Field | Type | Notes |
| --- | --- | --- |
| 类型 | select | risk, assumption, decision, dependency |
| 描述 | text | Description |
| 影响 | text | Impact |
| 证据 | text | Source evidence |
| 决策 | text | Decision if any |
| 负责人 | text | Owner if known |
| 状态 | select | open, reviewing, decided, closed |
