# Lark CLI Command Workflow

This file replaces the original helper scripts for RedSkill platforms that only import `.md` or `.txt`.

Run commands directly with `lark-cli`.

## 1. Create Project Overview

Create this Markdown content:

```markdown
# <项目名> - 项目总览

## 背景

待根据资料归档补充。

## 目标

待用户确认。

## 当前状态

- 阶段：<项目阶段>
- 工作流模式：initialize

## 关键资料

- <资料来源>

## 核心判断

待根据需求池、竞品矩阵和风险日志补充。

## 待确认事项

- 项目目标
- MVP 范围
- 需求优先级
- 负责人和排期

## 下一步行动

1. 归档资料到资料索引。
2. 提取需求到需求池。
3. 拆解任务到任务计划。
4. 更新风险与决策日志。

## 关联链接

创建完成后回填项目管理 Base 和白板 brief 链接。
```

Run:

```bash
lark-cli docs +create \
  --api-version v2 \
  --doc-format markdown \
  --content '<PROJECT_OVERVIEW_MARKDOWN>'
```

Record the returned document URL or token.

## 2. Create Project Management Base

Run:

```bash
lark-cli base +base-create \
  --name "<项目名> - 项目管理" \
  --time-zone Asia/Shanghai
```

Record the returned Base URL and token. The token may appear as `base_token`, `app_token`, `obj_token`, or `token`.

New Feishu Bases usually include a default empty table named like `数据表`. Do not delete it unless
the user explicitly asks. If the user asks to remove it, list tables first and confirm the exact
table id before deletion.

## 3. Create Tables

Use:

```bash
lark-cli base +table-create \
  --base-token "<BASE_TOKEN>" \
  --name "<TABLE_NAME>" \
  --fields '<FIELDS_JSON>'
```

### 资料索引 Fields JSON

```json
[
  { "name": "标题", "type": "text" },
  { "name": "类型", "type": "select", "multiple": false, "options": [
    { "name": "feedback" },
    { "name": "interview" },
    { "name": "PRD" },
    { "name": "meeting" },
    { "name": "competitor" },
    { "name": "chat" },
    { "name": "task" },
    { "name": "decision" }
  ]},
  { "name": "来源", "type": "text" },
  { "name": "摘要", "type": "text" },
  { "name": "关联对象", "type": "text" },
  { "name": "更新时间", "type": "date" }
]
```

### 需求池 Fields JSON

```json
[
  { "name": "需求", "type": "text" },
  { "name": "来源", "type": "text" },
  { "name": "用户证据", "type": "text" },
  { "name": "影响范围", "type": "select", "multiple": false, "options": [
    { "name": "用户" },
    { "name": "业务" },
    { "name": "技术" },
    { "name": "运营" },
    { "name": "待确认" }
  ]},
  { "name": "优先级", "type": "select", "multiple": false, "options": [
    { "name": "P0" },
    { "name": "P1" },
    { "name": "P2" },
    { "name": "P3" },
    { "name": "needs confirmation" }
  ]},
  { "name": "状态", "type": "select", "multiple": false, "options": [
    { "name": "new" },
    { "name": "reviewing" },
    { "name": "accepted" },
    { "name": "parked" },
    { "name": "rejected" }
  ]},
  { "name": "关联资料", "type": "text" }
]
```

### 竞品矩阵 Fields JSON

```json
[
  { "name": "竞品", "type": "text" },
  { "name": "定位", "type": "text" },
  { "name": "功能", "type": "text" },
  { "name": "定价", "type": "text" },
  { "name": "差异点", "type": "text" },
  { "name": "启发", "type": "text" },
  { "name": "风险", "type": "text" }
]
```

### 任务计划 Fields JSON

```json
[
  { "name": "任务", "type": "text" },
  { "name": "模块", "type": "text" },
  { "name": "负责人", "type": "text" },
  { "name": "优先级", "type": "select", "multiple": false, "options": [
    { "name": "P0" },
    { "name": "P1" },
    { "name": "P2" },
    { "name": "P3" }
  ]},
  { "name": "预估工时", "type": "text" },
  { "name": "开始日期", "type": "date" },
  { "name": "截止日期", "type": "date" },
  { "name": "状态", "type": "select", "multiple": false, "options": [
    { "name": "todo" },
    { "name": "doing" },
    { "name": "blocked" },
    { "name": "done" }
  ]}
]
```

### 风险与决策日志 Fields JSON

```json
[
  { "name": "类型", "type": "select", "multiple": false, "options": [
    { "name": "risk" },
    { "name": "assumption" },
    { "name": "decision" },
    { "name": "dependency" }
  ]},
  { "name": "描述", "type": "text" },
  { "name": "影响", "type": "text" },
  { "name": "证据", "type": "text" },
  { "name": "决策", "type": "text" },
  { "name": "负责人", "type": "text" },
  { "name": "状态", "type": "select", "multiple": false, "options": [
    { "name": "open" },
    { "name": "reviewing" },
    { "name": "decided" },
    { "name": "closed" }
  ]}
]
```

## 4. Decide Whiteboard Handling

Do not create a Feishu document that only contains a whiteboard prompt by default. A whiteboard brief is not a finished whiteboard.

If visual review material is useful, prepare this brief in the agent reply:

```markdown
# <项目名> - 项目全景白板 brief

把“<项目名>”做成一张飞书项目全景白板。

需要包含：

1. 项目背景
2. 目标用户与核心场景
3. 当前阶段：<项目阶段>
4. 关键机会点
5. MVP 范围
6. 主要风险
7. 下一步行动

要求：

- 只展示可公开汇报的信息
- 不展示原始私人资料
- 保留对项目总览文档、需求池、任务计划的链接说明
- 风格简洁专业，适合需求评审
```

Then:

- If `beautiful-feishu-whiteboard` is available, pass this brief to that skill and generate a real editable Feishu whiteboard.
- If it is not available, return the brief to the user and say it can be used with `beautiful-feishu-whiteboard`.
- Only create a Feishu document for the brief if the user explicitly asks to persist the prompt.

## 5. Backfill Links

Append created links to the project overview. If a real whiteboard was generated, include the whiteboard link. If only a brief was returned in chat, do not call it a whiteboard link.

```markdown
## 已创建工作区对象

- 项目管理 Base：<BASE_URL>
- 项目全景白板：<REAL_WHITEBOARD_URL_IF_CREATED>

### 多维表格

- 资料索引
- 需求池
- 竞品矩阵
- 任务计划
- 风险与决策日志
```

Run:

```bash
lark-cli docs +update \
  --api-version v2 \
  --doc "<PROJECT_OVERVIEW_DOC_URL_OR_TOKEN>" \
  --command append \
  --doc-format markdown \
  --content '<BACKFILL_MARKDOWN>'
```

## 6. Inspect Created Objects

Use these commands when reviewing the result:

```bash
lark-cli docs +fetch \
  --api-version v2 \
  --doc "<PROJECT_OVERVIEW_DOC_URL_OR_TOKEN>" \
  --doc-format markdown \
  --detail simple

lark-cli base +table-list \
  --base-token "<BASE_TOKEN>"

lark-cli base +record-list \
  --base-token "<BASE_TOKEN>" \
  --table-id "<TABLE_ID>"
```

Valid `docs +fetch --detail` values are `simple`, `with-ids`, and `full`.

## 7. Write Archive Records

Before writing records, confirm fields:

```bash
lark-cli base +field-list \
  --base-token "<BASE_TOKEN>" \
  --table-id "<TABLE_ID>"
```

Create a record with `record-upsert`. The JSON is a top-level field map; do not wrap it in `fields`.

```bash
lark-cli base +record-upsert \
  --base-token "<BASE_TOKEN>" \
  --table-id "<TABLE_ID>" \
  --json '{"字段名":"字段值","状态":"new"}'
```

For select fields, pass the option name:

```json
{
  "优先级": "P0",
  "状态": "reviewing"
}
```

For date fields, use:

```text
2026-06-06 00:00:00
```

The returned `record_id_list` contains record ids that can be used for later updates.

## 8. Advance Existing Records

Update an existing record by passing `--record-id`:

```bash
lark-cli base +record-upsert \
  --base-token "<BASE_TOKEN>" \
  --table-id "<TABLE_ID>" \
  --record-id "<RECORD_ID>" \
  --json '{"状态":"doing","负责人":"待确认"}'
```

After updates, append a short change summary to the project overview:

```bash
lark-cli docs +update \
  --api-version v2 \
  --doc "<PROJECT_OVERVIEW_DOC_URL_OR_TOKEN>" \
  --command append \
  --doc-format markdown \
  --content '<CHANGE_SUMMARY_MARKDOWN>'
```
