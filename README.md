# 量潮创始人工作记忆

创始人整合自我与自由创造的记忆空间。

## 目录

记忆按主题域分为多个记忆集；时间线、洞察与方向在各集内闭环，档案层统一在 `data/profile/` 并按用途分区：

```text
data/context/
├── default/            # 创业与个人主线记忆集
│   ├── 2026-09-27.md   # 当天日志，放集根便于手机端直接写
│   ├── journal/        # 历史日志（按日期平铺）
│   ├── profile/        # 已迁出：档案在 data/profile/（think / work / write）
│   ├── insight/        # 认知洞察（机制与规律，按证据分级）
│   ├── intention/      # 人机协作意图（对齐层：AI 提问的澄清、摩擦处的澄清）
│   ├── report/        # 报告（专题输出与实现状态沉淀，如 vibe-coding-methods）
│   └── roadmap/        # 主题路线图（目标含元目标 → 核心问题 → 已/待决策）
├── write/              # 写作主线记忆集（最早为 assets/fiction/创作谈/）
│   ├── journal/        # 创作日志
│   ├── profile/        # 已迁出：创作档案在 data/profile/write/（quanttide-profile-of-founder）
│   ├── insight/        # 创作认知洞察
│   ├── roadmap/        # 作品路线图（三部曲世界观 / 职场言情 / 重生言情）
│   └── README.md
├── .agents/skills/     # Agent Skill
├── AGENTS.md           # Agent 工作指南
└── CHANGELOG.md        # 变更日志
```

## 数据流

路线图、洞察与意图在同一记忆集内闭环；档案层允许跨集重组：

```text
<集>/journal/（日志）→ journal-to-roadmap   → <集>/roadmap/（主题路线图）
                    → journal-to-insight   → <集>/insight/（认知洞察）
                    → journal-to-intention → <集>/intention/（意图对齐）

<集>/journal/（日志）→ journal-to-profile  → data/profile/（档案，已迁出本仓）
```

档案按用途分区，不再与记忆集一一对应：

| 分区 | 收什么 | 来源 |
|------|--------|------|
| `think/` | 认知档案：怎么想、怎么应对 | 各集日志蒸馏后按事情重组 |
| `work/` | 事项台账：事实、决定与下一步 | 各集日志中的在办事项 |
| `write/` | 创作认知地图与创作档案 | `write/` 日志 |

同一集日志可同时贡献多个分区；`think/` 允许跨集重组，不要求与记忆集同名。

日志新增或修改后，四条蒸馏按各自 skill 自动执行，无需人工指示：

- 档案只收跨时间稳定的个人特征；决策、单次事件不进档案。
- 路线图只收方向层内容，按证据分级，以最新状态为准：目标（含元目标）→ 核心问题 → 已/待决策。
- 洞察只收可对错判断的命题（机制、规律、临界点），按证据分已确认/假说；感受、选择、事件不进洞察。
- 意图只收人机协作现场的澄清（AI 提问时的回答、交互摩擦处的「要 X，不要 Y」），按主题分文件与 insight/roadmap 对齐，沉淀为稳定判断归档案、成形为决策归路线图；目前仅 `default/` 启用。

## 文档边界

| 层级 | 目录 | 内容 |
|------|------|------|
| 时间线 | `<集>/`（当天）、`<集>/journal/`（历史） | 原始日志，按日期记录 |
| 特征 | `data/profile/`（已迁出本仓） | 蒸馏后的档案，按用途分 `think/`、`work/`、`write/` |
| 认知 | `<集>/insight/` | 想通的机制与规律命题，已确认/假说分级 |
| 方向 | `<集>/roadmap/` | 目标（含元目标）、核心问题、已/待决策 |
| 对齐 | `<集>/intention/` | 人机协作的意图对齐信息（目前仅 `default/`） |

## 相关文档

| 文档 | 用途 |
|------|------|
| [AGENTS.md](AGENTS.md) | 工作原则、Skill 索引、触发规则 |
| [CHANGELOG.md](CHANGELOG.md) | 版本变更记录 |
