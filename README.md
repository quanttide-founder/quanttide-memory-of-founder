# 量潮创始人工作记忆

创始人整合自我与自由创造的记忆空间。

## 目录

记忆按主题域分为两个记忆集，每个集内是同一套四层结构：

```text
assets/memory/
├── default/            # 创业与个人主线记忆集
│   ├── 2026-09-26.md   # 当天日志，放集根便于手机端直接写
│   ├── journal/        # 历史日志（按日期平铺）
│   ├── profile/        # 个人档案（从日志跨日期蒸馏）
│   │   ├── emotions.md    # 情绪
│   │   ├── values.md      # 价值观
│   │   ├── triggers.md    # 触发点
│   │   ├── methods.md     # 方法论（思维框架与应对策略）
│   │   └── expressions.md # 表达（叙事指纹）
│   ├── insight/        # 认知洞察（机制与规律，按证据分级）
│   ├── intention/      # 人机协作意图（对齐层：AI 提问的澄清、摩擦处的澄清）
│   └── roadmap/        # 主题路线图（目标含元目标 → 核心问题 → 已/待决策）
├── write/              # 写作主线记忆集（原 assets/fiction/创作谈/）
│   ├── journal/        # 创作日志
│   ├── profile/        # 创作档案（创作动机 / 创作方法 / 创作困境）
│   ├── insight/        # 创作认知洞察
│   ├── roadmap/        # 作品路线图（三部曲世界观 / 职场言情 / 重生言情）
│   └── README.md
├── .agents/skills/     # Agent Skill
├── AGENTS.md           # Agent 工作指南
└── CHANGELOG.md        # 变更日志
```

## 数据流

蒸馏在同一记忆集内闭环，不跨集搬运：

```text
<集>/journal/（日志）→ journal-to-profile  → <集>/profile/（个人档案）
                    → journal-to-roadmap   → <集>/roadmap/（主题路线图）
                    → journal-to-insight   → <集>/insight/（认知洞察）
                    → journal-to-intention → <集>/intention/（意图对齐）
```

日志新增或修改后，四条蒸馏按各自 skill 自动执行，无需人工指示：

- 档案只收跨时间稳定的个人特征；决策、单次事件不进档案。
- 路线图只收方向层内容，按证据分级，以最新状态为准：目标（含元目标）→ 核心问题 → 已/待决策。
- 洞察只收可对错判断的命题（机制、规律、临界点），按证据分已确认/假说；感受、选择、事件不进洞察。
- 意图只收人机协作现场的澄清（AI 提问时的回答、交互摩擦处的「要 X，不要 Y」），按主题分文件与 insight/roadmap 对齐，沉淀为稳定判断归档案、成形为决策归路线图；目前仅 `default/` 启用。

## 文档边界

| 层级 | 目录 | 内容 |
|------|------|------|
| 时间线 | `<集>/`（当天）、`<集>/journal/`（历史） | 原始日志，按日期记录 |
| 特征 | `<集>/profile/` | 蒸馏后的个人档案，跨日期稳定 |
| 认知 | `<集>/insight/` | 想通的机制与规律命题，已确认/假说分级 |
| 方向 | `<集>/roadmap/` | 目标（含元目标）、核心问题、已/待决策 |
| 对齐 | `<集>/intention/` | 人机协作的意图对齐信息（目前仅 `default/`） |

## 相关文档

| 文档 | 用途 |
|------|------|
| [AGENTS.md](AGENTS.md) | 工作原则、Skill 索引、触发规则 |
| [CHANGELOG.md](CHANGELOG.md) | 版本变更记录 |
