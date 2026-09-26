# 量潮创始人工作记忆

创始人的第二大脑记忆仓库：保存日志时间线、蒸馏后的个人档案与方向层文档。

## 目录

```text
assets/memory/
├── journal/           # 日志时间线（原始记录）
│   └── default/       # 默认日志，按日期分文件
├── profile/           # 个人档案（从日志跨日期蒸馏）
│   ├── emotions.md    # 情绪
│   ├── values.md      # 价值观
│   ├── triggers.md    # 触发点
│   ├── methods.md     # 方法论（思维框架与应对策略）
│   └── expressions.md # 表达（叙事指纹）
├── insight/           # 认知洞察（从日志提炼的机制与规律，按证据分级）
├── roadmap/           # 主题路线图（方向层：目标含元目标 → 核心问题 → 已/待决策）
├── .agents/skills/    # Agent Skill
├── AGENTS.md          # Agent 工作指南
└── CHANGELOG.md       # 变更日志
```

## 数据流

```text
journal/（日志）→ journal-to-profile  → profile/（个人档案）
               → journal-to-roadmap   → roadmap/（主题路线图）
               → journal-to-insight   → insight/（认知洞察）
```

日志新增或修改后，三条蒸馏按各自 skill 自动执行，无需人工指示：

- 档案只收跨时间稳定的个人特征；决策、单次事件不进档案。
- 路线图只收方向层内容，按证据分级，以最新状态为准：目标（含元目标）→ 核心问题 → 已/待决策。
- 洞察只收可对错判断的命题（机制、规律、临界点），按证据分已确认/假说；感受、选择、事件不进洞察。

## 文档边界

| 层级 | 目录 | 内容 |
|------|------|------|
| 时间线 | `journal/` | 原始日志，按日期记录 |
| 特征 | `profile/` | 蒸馏后的个人档案，跨日期稳定 |
| 认知 | `insight/` | 想通的机制与规律命题，已确认/假说分级 |
| 方向 | `roadmap/` | 目标（含元目标）、核心问题、已/待决策 |

## 相关文档

| 文档 | 用途 |
|------|------|
| [AGENTS.md](AGENTS.md) | 工作原则、Skill 索引、触发规则 |
| [CHANGELOG.md](CHANGELOG.md) | 版本变更记录 |
