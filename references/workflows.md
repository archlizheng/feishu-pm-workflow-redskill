# Workflow Selection

Use the smallest workflow that completes the user's request.

## Initialize

Use when the user starts a new project or asks to create a Feishu project workspace.

Steps:

1. Run the preflight commands from `SKILL.md`.
2. Collect project name, stage, available sources, and desired outputs.
3. Show the workspace plan before writing.
4. Create or reuse project objects with `lark-cli`.
5. Write the project overview, create one project management Base, then create the source index, requirement pool, competitor matrix, task plan, and risk/decision log tables inside it.
6. Prepare a whiteboard brief in the agent reply when visual review material is useful.
7. If `beautiful-feishu-whiteboard` is available, hand off the brief to create a real editable Feishu whiteboard.
8. Append the Base link and any real whiteboard link back to the project overview.
9. Return links, created objects, assumptions, and next commands.

## Archive

Use when the user already has local or Feishu materials.

Steps:

1. Identify material sources and target workspace.
2. Classify each source using `archive-rules.md`.
3. Extract summaries, requirements, risks, decisions, and tasks.
4. Use `base +field-list` to confirm fields, then write structured rows to the matching tables with `base +record-upsert`.
5. Update the project overview with a source summary.
6. Return an archive report and unresolved questions.

## Advance

Use when the workspace already exists and new information should update it.

Steps:

1. Read the new material.
2. Decide which objects are affected: source index, requirements, tasks, risks, decisions, PRD, report, or whiteboard.
3. Use `base +record-upsert --record-id` for record updates and `docs +update --command append` for overview changes.
4. Mark new, changed, and needs-confirmation items.
5. Return a change summary and suggested next action.

## One-Question Rule

If the mode is unclear, ask only:

```text
你希望我这次主要做“新项目初始化”，还是“整理已有项目资料”？
```
