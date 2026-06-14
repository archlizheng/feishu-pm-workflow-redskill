# feishu-pm-workflow RedSkill

`feishu-pm-workflow` 是一个面向产品经理和项目负责人的 RedSkill，用来通过 `lark-cli` 把一堆分散资料整理成一个可持续维护的飞书项目工作区。

它不是单纯的“帮你写 PRD”工具，而是一个 **飞书 PM 工作流编排 Skill**：把项目总览、资料归档、需求池、竞品分析、任务计划、风险决策和评审材料放到合适的飞书对象里。

## 它能做到什么

### 1. 初始化一个飞书项目工作区

你可以对 Agent 说：

```text
帮我为“AI 面试评估工具”初始化一个飞书 PM 工作区。
```

它会指导 Agent 创建：

- `项目总览` 飞书文档
- `项目管理` 多维表格 Base
- `资料索引` 表
- `需求池` 表
- `竞品矩阵` 表
- `任务计划` 表
- `风险与决策日志` 表

创建完成后，Agent 会把 Base 链接回填到项目总览文档里，让项目总览成为整个项目的入口。

### 2. 把已有资料系统化归档

适合处理这些资料：

- 本地 Markdown / 文档
- 飞书文档链接
- 会议纪要
- 用户访谈记录
- 用户反馈
- 竞品资料
- PRD 草稿
- 聊天记录
- 临时任务记录

它会帮助 Agent 判断资料类型，并提取到对应位置：

| 资料类型 | 提取内容 | 写入位置 |
| --- | --- | --- |
| 用户反馈 | 痛点、场景、情绪、证据强度 | 需求池 |
| 访谈记录 | 用户目标、行为、阻碍、引用证据 | 资料索引、需求池 |
| 竞品资料 | 定位、功能、定价、差异点 | 竞品矩阵 |
| 会议纪要 | 决策、待办、风险、负责人 | 风险与决策日志、任务计划 |
| PRD 草稿 | 背景、范围、功能点、指标 | 项目总览、任务计划 |

### 3. 维护项目推进状态

项目创建后，你可以继续让 Agent 更新它：

```text
把这份用户反馈归入需求池。
根据 PRD 拆任务并同步到多维表格。
根据今天的会议纪要更新项目状态。
更新风险日志，并列出需要我确认的决策。
生成本周项目评审摘要。
```

Skill 会指导 Agent 使用 `lark-cli base +record-upsert` 创建或更新记录，并把关键推进摘要追加到项目总览文档。

### 4. 为评审白板准备 brief

当项目需要评审或汇报时，它可以生成一段白板 brief，例如：

```text
把当前项目状态做成一张飞书项目全景白板，包含背景、目标用户、MVP 范围、主要风险、关键决策和下一步行动。
```

注意：**白板 brief 不是已生成的飞书画板**。

如果你的环境里有 `beautiful-feishu-whiteboard`，可以把 brief 交给它生成真实、可编辑的飞书白板。`feishu-pm-workflow` 负责项目编排，`beautiful-feishu-whiteboard` 负责视觉表达。

## 适合哪些场景

- 产品经理启动一个新项目
- 创业团队整理前期调研资料
- 把本地 PRD、会议纪要、竞品分析同步到飞书
- 把项目需求和任务从聊天记录里沉淀出来
- 为需求评审或项目周会准备结构化资料
- 用飞书 CLI 展示“AI Agent 如何接管 PM 重复工作流”

## 不适合做什么

这个 Skill 不是：

- 自动替你做最终产品决策的工具
- 单点 PRD 写作器
- 真实白板生成器
- 项目管理系统的完整替代品
- 无需人工 review 的自动化发布工具

它会把 AI 推断的优先级、范围、负责人、时间计划标记为 `needs confirmation` 或“待确认”，关键判断仍然需要产品负责人 review。

## 生成的飞书结构

默认结构如下：

```text
<项目名> - 项目总览
<项目名> - 项目管理
```

`<项目名> - 项目管理` 是一个飞书多维表格 Base，里面包含：

```text
资料索引
需求池
竞品矩阵
任务计划
风险与决策日志
```

默认不会创建“白板 brief 文档”。白板 brief 会先在 Agent 回复里生成；只有用户明确要求保存 brief，才会写入飞书文档。

## 使用前提

你需要：

- Node.js 20+
- 已安装 `lark-cli`
- 已登录并授权飞书 / Lark 账号

检查命令：

```bash
node -p 'Number(process.versions.node.split(".")[0])'
lark-cli --help
lark-cli auth status
```

如果还没安装：

```bash
npm install -g @larksuite/cli
lark-cli config init
lark-cli auth login
```

## 安装方式

本仓库是 RedSkill 兼容版本：保留文件夹结构，但所有核心文件都是 `.md`，适合只能导入 `.md` / `.txt` 的平台。

### 方式一：导入 RedSkill 平台

1. 打开 GitHub 仓库：[https://github.com/archlizheng/feishu-pm-workflow-redskill](https://github.com/archlizheng/feishu-pm-workflow-redskill)
2. 下载仓库 ZIP，或将仓库导入到 RedSkill 平台。
3. 上传整个 `feishu-pm-workflow` 文件夹。
4. 确认平台能够读取根目录下的 `SKILL.md` 和 `references/` 目录。

目录结构：

```text
feishu-pm-workflow/
├── README.md
├── SKILL.md
├── LICENSE.md
└── references/
    ├── archive-rules.md
    ├── lark-cli-commands.md
    ├── object-schemas.md
    ├── prd-template.md
    ├── whiteboard-briefs.md
    └── workflows.md
```

### 方式二：安装到 Codex / Agents 本地 Skill 目录

如果你的 Agent 使用 `~/.agents/skills` 作为 Skill 目录，可以直接 clone：

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/archlizheng/feishu-pm-workflow-redskill.git ~/.agents/skills/feishu-pm-workflow
```

更新到最新版本：

```bash
cd ~/.agents/skills/feishu-pm-workflow
git pull
```

### 方式三：安装到 Claude Code 本地 Skill 目录

如果你在 Claude Code 中使用本地 Skill，可以 clone 到 `~/.claude/skills`：

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/archlizheng/feishu-pm-workflow-redskill.git ~/.claude/skills/feishu-pm-workflow
```

更新到最新版本：

```bash
cd ~/.claude/skills/feishu-pm-workflow
git pull
```

### 安装后验证

在 Agent 中输入类似指令：

```text
使用 feishu-pm-workflow，帮我为“AI 面试评估工具”初始化一个飞书 PM 工作区。
```

如果 Agent 能识别该 Skill，并在执行前检查 `lark-cli`、飞书登录状态和项目写入计划，说明安装成功。

## 文件结构

```text
feishu-pm-workflow/
├── README.md
├── SKILL.md
├── LICENSE.md
└── references/
    ├── archive-rules.md
    ├── lark-cli-commands.md
    ├── object-schemas.md
    ├── prd-template.md
    ├── whiteboard-briefs.md
    └── workflows.md
```

## 文件说明

- `SKILL.md`：Skill 入口，定义触发条件、工作流、边界和交付规则。
- `LICENSE.md`：MIT 开源协议。
- `references/workflows.md`：初始化、归档、推进三种模式。
- `references/object-schemas.md`：飞书文档和多维表格字段结构。
- `references/lark-cli-commands.md`：创建文档、Base、表、记录更新的命令说明。
- `references/archive-rules.md`：资料分类和归档规则。
- `references/prd-template.md`：项目 Brief 和 PRD 模板。
- `references/whiteboard-briefs.md`：白板 brief 和 `beautiful-feishu-whiteboard` 交接规则。

## 安全设计

- 默认先规划，再写入。
- 不会默认删除飞书对象。
- 新建 Base 后出现的默认空表不会自动删除，除非用户明确要求。
- 保留资料来源，避免把证据压缩成不可追溯总结。
- 白板 brief 不会被冒充为真实白板。
- 涉及范围、优先级、负责人、排期的判断会标记为待确认。

## 版本状态

当前版本：`1.0.0-redskill`

该版本已经过真实飞书场景测试：可初始化项目工作区、创建 Base 和 5 张表、写入资料/需求/任务/风险记录，并更新项目总览。

## 开源协议

本项目基于 MIT License 开源。你可以自由使用、复制、修改、分发和二次开发，但需要保留原始版权声明和协议文本。详见 [LICENSE.md](LICENSE.md)。
