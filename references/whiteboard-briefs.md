# Whiteboard Briefs

Use this file when preparing content for visual review or for `beautiful-feishu-whiteboard`.

Important: a whiteboard brief is not a finished whiteboard. By default, return the brief in the agent reply. If `beautiful-feishu-whiteboard` is available, hand off the brief to that skill and create a real editable Feishu whiteboard. Create a Feishu document containing only the brief only when the user explicitly asks to persist it.

## When To Create A Whiteboard

Create a whiteboard brief for:

- project overview
- discovery report
- competitor analysis
- requirement review
- roadmap
- retrospective

Do not create a whiteboard for raw evidence archives or daily task management.

## Project Overview Brief

```text
把“<项目名>”做成一张飞书项目全景白板。

需要包含：
1. 项目背景
2. 目标用户与核心场景
3. 当前阶段
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

## Discovery Brief

```text
把这轮前期调研做成一张飞书画板。

需要包含：
1. 用户痛点聚类
2. 竞品分层
3. 机会点
4. MVP 建议
5. 风险假设
6. 待验证问题
```

## Return Contract

If a real whiteboard is created, link it back to:

- project overview doc
- related source index rows
- requirement pool or task plan when relevant

If no real whiteboard is created, say clearly:

```text
以下是白板生成 brief，不是已生成的飞书画板。
```
