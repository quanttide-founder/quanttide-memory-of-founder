# AGENTS.md

量潮创始人第二大脑的记忆仓库：日志时间线、个人档案、方向决策。

## 记忆集

记忆按主题域分集存放。每个记忆集是一套独立的四层结构，`journal/ profile/ insight/ roadmap/` 四个目录名在各集内保持一致，层内文件由各集按自身主题定义。

| 记忆集 | 主题域 | 说明 |
|--------|--------|------|
| `default/` | 创业与个人主线 | 业务、平台、认知与日常日志；档案为五轴（emotions / values / triggers / methods / expressions） |
| `write/` | 写作主线 | 创作日志、创作档案（创作动机 / 创作方法 / 创作困境）、作品路线图；原 `assets/fiction/创作谈/` |

**分集规则**：

- 写入前先判定主题域归哪个集；两集都像时归 `default/`。
- 蒸馏只在同一记忆集内闭环：某集的日志只产出该集的档案、路线图与洞察，不跨集搬运。
- 记忆集之间不互设依赖，单集可独立删除或归档。

## 目录与边界

| 层级 | 目录 | 内容特征 | 示例 |
|------|------|---------|------|
| 时间线 | `<集>/journal/` | 原始日志，按日期记录 | 新增/修改日志 |
| 特征 | `<集>/profile/` | 跨日期蒸馏的稳定特征 | 情绪、价值观、触发点、方法论、表达 |
| 认知 | `<集>/insight/` | 想通的机制与规律命题，按证据分级 | 已确认、假说 |
| 方向 | `<集>/roadmap/` | 愿景、选择、待定方向 | 目标（含元目标）、核心问题、已决策、待决策 |

**边界规则**：
- 单次事件与业务状态不进 `<集>/profile/`，也不进 `<集>/insight/` 与 `<集>/roadmap/`——它们只存在于 `<集>/journal/` 时间线中。
- 认识三分：想通的命题归 `<集>/insight/`；命题反复套用成思维框架后归 `<集>/profile/` 中的方法论文件；命题引出的选择归 `<集>/roadmap/`。同一认识只在一处完整展开，跨层只留互链。
- 决策（无论已/待）归 `<集>/roadmap/`；元目标是目标的子层，随目标归 `<集>/roadmap/`；跨时间稳定的个人特征归 `<集>/profile/`。
- `<集>/profile/` 只描述特征，不给建议；建议是对话输出，不是档案内容。
- **日志落位**：当天日志直接放在记忆集根部（如 `default/2026-09-26.md`），便于在手机端直接写入；更早的日志平铺在 `<集>/journal/YYYY-MM-DD.md`。不设按来源的中间层目录。

## 工作流

### 触发规则

- **日志更新后蒸馏档案**：`<集>/journal/` 中新增或修改日志后，读取 `.agents/skills/journal-to-profile/SKILL.md` 并按其流程更新**同一集** `<集>/profile/` 下的档案，无需用户再次指示。
- **日志更新后更新路线图**：同一时机，读取 `.agents/skills/journal-to-roadmap/SKILL.md` 并按其流程更新同一集 `<集>/roadmap/` 下的主题路线图，无需用户再次指示。
- **日志更新后提炼洞察**：同一时机，读取 `.agents/skills/journal-to-insight/SKILL.md` 并按其流程更新同一集 `<集>/insight/` 下的认知洞察，无需用户再次指示。

### Skill 索引

| Skill | 用途 | 路径 |
|-------|------|------|
| `journal-to-profile` | 从日志蒸馏个人档案 | `.agents/skills/journal-to-profile/SKILL.md` |
| `journal-to-roadmap` | 从日志蒸馏方向层路线图 | `.agents/skills/journal-to-roadmap/SKILL.md` |
| `journal-to-insight` | 从日志提炼认知洞察 | `.agents/skills/journal-to-insight/SKILL.md` |

## 工作原则

### 最小干预
- 仅在用户明确请求时操作
- 不主动创建文件（除非必要）
- 优先编辑现有文件

### 原子提交
- 每次提交独立完整
- 不提交不完整的更改
- 验证后再提交

### 验证优先
- 修改后运行构建验证
- 确保更改符合预期

## 输出规范

### 内容格式
- 不使用 emoji（除非用户明确请求）
- 输出简洁，适合 CLI 显示

### 文件引用
- 使用 `code` 格式表示文件路径
- 每个引用独立，不合并

## Git 提交规范

遵循 Conventional Commits 格式：

| 类型 | 说明 |
|------|------|
| `docs` | 文档更新 |
| `refactor` | 重构 |
| `chore` | 构建/工具 |

## Skill 维护

| 类型 | 写在哪里 |
|------|---------|
| 详细说明、工作流步骤 | `.agents/skills/` 中的 Skill 文件 |
| 给链接、导航索引 | AGENTS.md |

### 新建 Skill

```bash
mkdir -p .agents/skills/<name>
# 创建 .agents/skills/<name>/SKILL.md
```

SKILL.md 模板：

```markdown
---
name: <name>
description: 功能描述。
---

# <name>

## 规则

- 必须遵守的约束

## 工作流

### 步骤名称

操作步骤
```

`name` 必须与目录名一致。新建后在本文件的 Skill 索引中登记；若有自动触发场景，同步在工作流的触发规则中挂载。

### 修改 / 删除 Skill

直接编辑 `.agents/skills/<name>/SKILL.md`；删除用 `rm -rf .agents/skills/<name>`，同时清理本文件中的索引与触发规则条目。
