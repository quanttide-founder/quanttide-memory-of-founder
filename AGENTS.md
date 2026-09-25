# AGENTS.md

量潮创始人第二大脑的记忆仓库：日志时间线、个人档案、方向决策。

## 目录与边界

| 层级 | 目录 | 内容特征 | 示例 |
|------|------|---------|------|
| 时间线 | `journal/` | 原始日志，按日期记录 | 新增/修改日志 |
| 特征 | `profile/` | 跨日期蒸馏的稳定特征 | 情绪、价值观、触发点、方法论、表达 |
| 方向 | `roadmap/` | 愿景、选择、待定方向 | 目标、已决策、待决策、核心问题、元目标 |

**边界规则**：
- 单次事件与业务状态不进 `profile/`，也不进 `roadmap/`——它们只存在于 `journal/` 时间线中。
- 决策（无论已/待）与元目标归 `roadmap/`；跨时间稳定的个人特征归 `profile/`。
- `profile/` 只描述特征，不给建议；建议是对话输出，不是档案内容。

## 工作流

### 触发规则

- **日志更新后蒸馏档案**：`journal/` 中新增或修改日志后，读取 `.agents/skills/journal-to-profile/SKILL.md` 并按其流程更新 `profile/` 下的档案（emotions / values / triggers / methods / expressions），无需用户再次指示。
- **日志更新后更新路线图**：同一时机，读取 `.agents/skills/journal-to-roadmap/SKILL.md` 并按其流程更新 `roadmap/` 下的主题路线图，无需用户再次指示。

### Skill 索引

| Skill | 用途 | 路径 |
|-------|------|------|
| `journal-to-profile` | 从日志蒸馏个人档案 | `.agents/skills/journal-to-profile/SKILL.md` |
| `journal-to-roadmap` | 从日志蒸馏方向层路线图 | `.agents/skills/journal-to-roadmap/SKILL.md` |

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
