# Changelog

## [1.2.1] - 2026-09-26

### Added

- `.agents/skills/journal-to-intention/`：从日志提取人类意图写入 `<集>/intention/`，收录 AI 提问时人类的回答与交互摩擦处的主动澄清，用于对齐人机协作信息
- `default/intention/`：`default/` 记忆集的对齐层，首发 `ai.md` 七条人机协作意图（`write/` 集暂不启用）
- AGENTS.md、README.md：目录边界、边界规则、数据流与触发规则登记 `intention/` 层及 `journal-to-intention` skill

## [1.2.0] - 2026-09-26

**定位说明**：记忆仓库由「单记忆集四层平铺」改为「多记忆集」架构。顶层按主题域划分为记忆集，每个记忆集内保持 `journal/ profile/ insight/ roadmap/` 同构四层；蒸馏在同一集内闭环，不跨集搬运。同时从 `assets/fiction` 收编创作记忆，建立 `write/` 记忆集。

### 破坏性变更与迁移指南

所有原有路径整体下沉一层，原根级四层目录即 `default/` 记忆集；原 `journal/default/` 中间层被摊平进 `default/journal/`。按旧路径读取或写入会落空，需按下表迁移：

| 旧路径 | 新路径 |
|--------|--------|
| `journal/YYYY-MM-DD.md` | `default/YYYY-MM-DD.md`（集根，当天） |
| `journal/default/YYYY-MM-DD.md` | `default/journal/YYYY-MM-DD.md`（历史） |
| `profile/{emotions,values,triggers,methods,expressions}.md` | `default/profile/` 同名 |
| `insight/{business,platform,ai,creative}.md` | `default/insight/` 同名 |
| `roadmap/{business,platform,creative}.md` | `default/roadmap/` 同名 |
| `assets/fiction/创作谈/**` | `write/**`（跨子模块） |

AGENTS.md、README.md 与 `journal-to-*` 三个 skill 已同步改为 `<集>/` 前缀写法，并新增分集规则：写入前判定主题域，两集都像时归 `default/`；蒸馏不跨集。

### Added

- `write/`：写作记忆集，收录创作日志（2026-09-05 ~ 2026-09-25）、创作档案（创作动机 / 创作方法 / 创作困境）、创作认知洞察与作品路线图（三部曲世界观 / 职场言情 / 重生言情），迁自 `assets/fiction/创作谈/`
- AGENTS.md「记忆集」节：分集表、分集规则与四层同构约定

### Changed

- 顶层结构：根级 `journal/ profile/ insight/ roadmap/` 下沉为 `default/` 记忆集
- `journal/`：取消按来源的 `default/` 中间层；当天日志置于集根，历史日志平铺于 `<集>/journal/`
- AGENTS.md 新增「日志落位」规则：当天日志放集根便于手机端直接写入，更早日志归 `<集>/journal/`
- AGENTS.md、README.md：目录边界、数据流与触发规则改为 `<集>/` 前缀，触发规则明确蒸馏限同一记忆集内
- `.agents/skills/journal-to-{profile,roadmap,insight}/SKILL.md`：扫描范围改为本集全部日志且不读其他集，输出路径改为 `<集>/` 前缀，按集举例
- `.agents/skills/journal-to-profile/SKILL.md`：参照口吻的路径由 `../fiction/草稿箱/2_情绪日记/` 修正为 `../fiction/观察站/1_情绪日记/`

### Removed

- 根级 `journal/`、`profile/`、`insight/`、`roadmap/` 目录（迁入 `default/`，路径见上表）
- `journal/default/` 中间层（摊平进 `default/journal/`）

## [1.1.1] - 2026-09-26

认知洞察层：新增 journal-to-insight skill，日志经第三条蒸馏管线产出 `insight/` 认知洞察（已确认/假说分级），时间线 → 特征/认知/方向的分层成形。

### Added

- `insight/`：认知洞察首批（business / platform / ai / creative），8 条命题按已确认/假说分级
- `.agents/skills/journal-to-insight/`：日志提炼认知洞察 skill（三问过滤 + 命题判据 + 证据分级 + 跨层晋升规则）
- AGENTS.md 触发规则：日志更新后自动执行三蒸馏（档案 / 路线图 / 洞察）

### Changed

- AGENTS.md、README.md：目录边界与数据流补充认知层，Skill 索引登记 journal-to-insight
- `roadmap/creative.md`：新增待决策「memory→fiction 链路打通」（来自 09-26 日志蒸馏）
- `profile/expressions.md`：「从记忆到小说」机制命题移入 `insight/creative.md`，原处改留导引

## [1.1.0] - 2026-09-26

个人档案与双蒸馏管线：日志经显式提炼层蒸馏为个人档案（特征）与主题路线图（方向），两条蒸馏均由 skill 规范并挂载自动触发。

### Added

- `profile/`：五轴个人档案（emotions 情绪 / values 价值观 / triggers 触发点 / methods 方法论 / expressions 表达）
- `roadmap/`：主题路线图首批（business / platform / creative），章节序为目标（含元目标）→ 核心问题 → 已/待决策
- `.agents/skills/journal-to-profile/`：日志蒸馏个人档案 skill
- `.agents/skills/journal-to-roadmap/`：日志蒸馏方向路线图 skill
- AGENTS.md 触发规则：日志更新后自动执行双蒸馏
- `journal/`：2026-08-10 ~ 2026-09-25 日报

### Changed

- AGENTS.md：重组为目录边界 → 工作流 → 行为约束结构，Skill 索引与触发规则统一挂载
- README.md：重写，补充目录结构与双分支数据流

### Removed

- `roadmap/qtfounder.md`：迁移至 `apps/qtfounder/ROADMAP.md`（平台路线图归所属应用仓库）
- `journal/default/` 2026-07-29 ~ 2026-09-19 共 53 篇归档至 `assets/archive/journal/default/`
- `insight/`、`context/` 笔记迁出（分别至 quanttide-tech 与 laboratory docs）
- `intention/`、`report/` 过时文件，`handbook/` 部分文档移出，voice-input 与战棋推演文档清理

## [1.0.0] - 2026-08-10

首个正式发布（1.0.0）：report 与 roadmap 目录结构扁平化后趋于稳定，后续遵循语义化版本规范，破坏性变更将单独声明。

### Added

- journal/: 2026-06-28 ~ 2026-08-09 日报
- report/voice-input.md: 语音输入安装状态与硬件诊断报告
- roadmap/voice-input.md: 语音输入路线图
- roadmap/index.md: 路线图索引
- context/: ai-native-work.md、fiction.md、meta.md、qtgame-war.md 语境文档

### Changed

- report/game/ 与 roadmap/game/ 目录扁平化（破坏性变更）
  - report/game/qtgame-war.md → report/qtgame-war.md
  - report/game/qtgame-weiqi.md → report/qtgame-weiqi.md
  - roadmap/game/qtgame-war.md → roadmap/qtgame-war.md
  - roadmap/game/qtgame-weiqi.md → roadmap/qtgame-weiqi.md
- roadmap/qtgame-war.md: 路线图简化

### Removed

- roadmap/game/index.md

## [0.5.2] - 2026-06-28

### Removed

- `journal/default/`：27 篇 6 月日记归档至 `assets/archive/journal/default/`

### Added

- `journal/2026-06-28.md`：今日日记

## [0.5.1] - 2026-06-28

### Added

- `report/` 目录：存放项目状态报告（事实层），与 roadmap（方向层）分离
  - `report/game/qtgame-war.md`：战旗游戏状态报告
  - `report/game/qtgame-weiqi.md`：围棋游戏状态报告
  - `report/fiction.md`：小说创作状态报告（骨架）

### Changed

- `roadmap/game/qtgame-war.md`：移除当前状态，按方向/事实分层重构，新增已决策/待决策节
- `roadmap/game/qtgame-weiqi.md`：移除当前状态，引用 report
- `AGENTS.md`：新增文档结构划分规范（roadmap vs report）

## [0.5.0] - 2026-06-27

### Added

- `journal/default/` 子目录，按来源组织日报
- 6/19 ~ 6/27 日报
- `library/motif.md` 和 `library/motif-vs-style.md` 文库文档
- `context/write.md` 写作工作语境
- `roadmap/qtcloud-write.md` 写作云蓝图

### Changed

- journal 目录结构改为按来源子目录分类

## [0.4.3] - 2026-05-08

### Added

- journal/default/2026-05-06.md: 新增日报
- journal/default/2026-05-07.md: 新增日报
- journal/media/2026-05-06.md: 新增媒体日报
- journal/qtconsult/2026-05-07.md: 新增咨询日报
- index.md: 新增索引文档

## [0.4.2] - 2026-05-06

### Added

- journal/2026-05-06.md: 新增日报

### Removed

- journal/default/, journal/product/, journal/game/, journal/qtcloud/: 归档至 archive 子仓库

## [0.4.1] - 2026-05-06

### Added

- roadmap/: 新增书茂 App 评论视频蓝图
- journal/media/2026-05-06.md: 新增媒体日报

### Changed

- journal/2026-05-05.md → journal/default/2026-05-05.md: 日报移至 default 子目录

### Removed

- ROADMAP.md: 移除已完成项

## [0.4.0] - 2026-05-05

### Added

- report/: 新增 report/write/ 和 report/default/，存放写作日志和日报
- essay/agent/: 转移并整理 agent 相关文档
- essay/think/: 新增认知工程文档
- profile/write/: 新增写作风格文档
- profile/game/: 新增游戏相关个人资料

### Removed

- report/default/: 将日报归档至 docs/archive 子仓库
- report/write/2026-05-03.md: 归档写作日志
- example/trouble.html, gallery/README.md, platform/README.md: 清理过时文件
- bylaw/org.md: 移除组织章程
- story/content-recommendation-algorithm.md: 移除内容推荐算法文档
- roadmap/qtcloud/qtcloud-think.md: 蓝图移至 vision
- vision/asset/, vision/media/: 移除废弃愿景资产

### Changed

- report/write/qtclass-platform-essay.md → report/write/2026-05-03.md: 文件命名规范化
- roadmap/ → vision/: 蓝图内容迁移至愿景层
- tutorial/harness_engineering.md → essay/agent/harness_engineering.md
- tutorial/cognitive_engineering.md → essay/think/cogntive_engineering.md
- gallery/write/sdr-style.md → profile/write/style.md

### Daily

- journal/: 2026-04-29 ~ 2026-05-05 日报归档

## [0.3.1] - 2026-04-29

### Added

- vision/default/: 新增 vision 层基础文档
  - vision/default/index.md: 愿景总览
  - vision/default/media.md: 媒体愿景
  - vision/default/org.md: 组织愿景
  - vision/default/pr.md: PR 策略
  - vision/default/qtclass.md: QtClass 愿景
  - vision/default/strategy.md: 战略愿景

## [0.3.0] - 2026-04-29

### Added

- context/: 从 context 子仓库接收大量文档，集中存放语境层内容
  - context/acadmics/, context/agent/, context/brand/, context/code/, context/course/
  - context/fiction/, context/health/, context/hr/, context/infra/, context/knowl/
  - context/media/, context/mkt/, context/product/, context/qtclass/, context/think/, context/write/
- bylaw/org.md: 组织章程
- context/think/: 新增 mental-models.md, situation-awareness.md, situation-level.md, refactor.md, role.md
- context/write/: 新增 brochure-style.md, story-style.md（替换 style.md）
- context/health/shame.md: 羞耻感分析
- context/media/: 新增 content.md, growth.md, role.md, strategy.md, workflow.md
- gallery/sdr-write-style.md: SDR 写作风格
- profile/think_pattern.md: 思考模式文档

### Removed

- context/asset/category.md, context/asset/index.md
- context/qtcloud-think/ixd.md
- context/write/style.md（拆分为 brochure-style.md 和 story-style.md）
- example/qtcloud-think/cogitive_prism.html

### Changed

- AGENTS.md: 更新工作原则
- roadmap/qtcloud/qtcloud-think.md: 更新愿景与路线图

### Daily

- journal/: 2026-04-26 ~ 2026-04-29 日报归档

## [0.2.2] - 2026-04-26

### Changed

- qtcloud-think.md: 重构愿景和蓝图分离
  - vision/qtcloud/: 重构愿景层（default, qtadmin, qtcloud-* 系列）
  - roadmap/qtcloud/qtcloud-think.md: 核心功能、方法论、冷启动路径
  - tutorial/: 新增认知工程和驾驭工程教程
  - cognitive_engineering.md: 认知工程方法论
  - harness_engineering.md: 驾驭工程教程

### Structure

- Roadmap 结构调整: roadmap/ 目录结构优化
- Vision 结构调整: 愿景层与蓝图层分离

## [0.2.1] - 2026-04-25

### Changed

- qtcloud-think.md: 重构愿景和蓝图分离
  - vision/qtcloud/qtcloud-think.md: 定位、原则、哲学、交互设计、运行循环、独特价值、愿景
  - roadmap/qtcloud/qtcloud-think.md: 工作流、核心功能、方法论、冷启动路径

## [0.2.0] - 2026-04-25

### Added
- qtcloud-think.md: 整合思考云产品愿景（关联联想、高频问题、思考模型）
- visualization.md: 数据可视化方案
- sync.md: 协作同步机制
- internal-training.md: 内部培训蓝图
- contract.yaml: 契约配置文件

### Changed
- 重构分类理论文档：why_category_theory_work.md, category_theory_on_story.md
- 优化资产规范：asset.md → asset_spec.md
- 扩展写作风格指南：fiction_style.md, style.md
- 更新日报归档（2026-04-19 ~ 2026-04-25）

### Structure
- 新增蓝图层：roadmap/ 目录结构
- 重构语境层：context/data/, context/think/
- 优化愿景层：vision/qtcloud/

### Process
- 新增技能：逆向拆解代码生成文档 SKILL
- 完善工作流：workflow.md, delib.md
- 归档废弃文件：gallery.md, qtcloud-asset.md

## [0.1.0] - 2026-04-19

### Added
- asset-classify skill: 资产分类技能，包含 Type/Category 双轴治理模型
- CONTRIBUTING.md: 维护指南
- AGENTS.md: Agent 配置索引

### Changed
- 重构分类结构，日志/蓝图/语境/愿景/归档六类

### Structure
- .agents/skills/asset-classify/SKILL.md
- CONTRIBUTING.md
- AGENTS.md
