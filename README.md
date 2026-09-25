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
├── roadmap/           # 方向层：愿景、决策、核心问题
├── .agents/skills/    # Agent Skill
├── AGENTS.md          # Agent 工作指南
└── CHANGELOG.md       # 变更日志
```

## 数据流

```text
journal/（日志）→ journal-to-profile skill → profile/（档案）
```

日志新增或修改后，按 `.agents/skills/journal-to-profile/SKILL.md` 蒸馏进五轴档案，无需人工指示。蒸馏只收跨时间稳定的特征：决策归 `roadmap/`，业务状态与待定决策不进档案。

## 文档边界

| 层级 | 目录 | 内容 |
|------|------|------|
| 时间线 | `journal/` | 原始日志，按日期记录 |
| 特征 | `profile/` | 蒸馏后的个人档案，跨日期稳定 |
| 方向 | `roadmap/` | 愿景、已/待决策、元目标 |

## 相关文档

| 文档 | 用途 |
|------|------|
| [AGENTS.md](AGENTS.md) | 工作原则、Skill 索引、触发规则 |
| [CHANGELOG.md](CHANGELOG.md) | 版本变更记录 |
