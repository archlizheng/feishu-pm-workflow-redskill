# Archive Rules

Classify every source before extracting data.

| Source Type | Extract | Destination |
| --- | --- | --- |
| 用户反馈 | pain, scene, sentiment, evidence strength | 需求池 |
| 访谈记录 | goal, behavior, blocker, quotes | 资料索引, 需求池 |
| 竞品资料 | positioning, feature, pricing, differentiation | 竞品矩阵 |
| 会议纪要 | decision, todo, risk, owner | 风险与决策日志, 任务计划 |
| PRD 草稿 | background, scope, feature, metric | 项目总览, PRD, 任务计划 |
| 聊天记录 | hidden need, dispute, pending question | 资料索引, 风险与决策日志 |

## Extraction Rules

- Before writing to a table, run `lark-cli base +field-list` to confirm real field names and writable field types.
- Create records with `lark-cli base +record-upsert --json '<FIELD_MAP_JSON>'`; the JSON must be a top-level field map.
- Keep one row per atomic requirement, risk, decision, or task.
- Preserve file path or Feishu link in the source field.
- Do not collapse contradictory evidence. Record conflicts as risks or pending decisions.
- If priority is inferred, set priority to `needs confirmation`.
- If owner or deadline is missing, leave it blank and include it in the confirmation list.

## Archive Report

Return:

```text
归档资料数量
新增需求数量
新增风险数量
新增任务数量
新增决策数量
需要用户确认的问题
```
