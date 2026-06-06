# feishu-pm-workflow RedSkill

`feishu-pm-workflow` helps an AI agent initialize, organize, archive, and maintain a Feishu/Lark PM workspace with `lark-cli`.

This repository is the RedSkill-compatible version: it keeps a folder structure, but all skill files are Markdown so platforms that only import `.md` or `.txt` files can use it.

## What It Creates

The default workflow creates:

- a project overview document
- one Feishu Base app named `<项目名> - 项目管理`
- five Base tables:
  - `资料索引`
  - `需求池`
  - `竞品矩阵`
  - `任务计划`
  - `风险与决策日志`
- an optional whiteboard handoff brief for `beautiful-feishu-whiteboard`

The skill does not pretend that a whiteboard brief is a real whiteboard. If `beautiful-feishu-whiteboard` is available, hand off the brief to generate an editable Feishu whiteboard.

## Requirements

- Node.js 20+
- `lark-cli`
- authenticated Feishu/Lark account

Preflight:

```bash
node -p 'Number(process.versions.node.split(".")[0])'
lark-cli --help
lark-cli auth status
```

## Import

Upload or import this folder into a RedSkill-compatible platform:

```text
feishu-pm-workflow/
├── SKILL.md
└── references/
    ├── archive-rules.md
    ├── lark-cli-commands.md
    ├── object-schemas.md
    ├── prd-template.md
    ├── whiteboard-briefs.md
    └── workflows.md
```

## Safety

- The skill creates new Feishu objects only after planning or confirmation.
- It does not delete the default empty Base table unless the user explicitly asks.
- It keeps source evidence traceable.
- It marks inferred priority, scope, ownership, and timing decisions as `needs confirmation`.

## Status

Version: `1.0.0-redskill`
