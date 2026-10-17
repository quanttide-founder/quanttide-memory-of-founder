collab —— 人机协作偏差与规则工具

先定一条架构线：HTTP API 是唯一真相，CLI 只是它的客户端。 CLI 不做业务逻辑，只负责参数解析、调 API、格式化输出。这样以后加 MCP 适配、加 skill 调用，都是同一层薄封装，不会出现三套逻辑。

```
skill / CLI / MCP  →  HTTP API  →  SQLite
```

一、命令结构（gh 风格 noun-verb）

```
collab deviation log        记录一条偏差
collab deviation list       列出偏差
collab deviation show <id>  单条详情
collab deviation similar    查同类偏差
collab rule list            列规则
collab rule promote         把偏差提升为规则
collab rule candidates      找重复 ≥2 次的偏差类别
collab schema [path]        输出 JSON Schema
collab config               查看/设置 server 地址
```

选 noun-verb 而不是 collab log，是为了让模型能从名字预测结构——和 gh pr view、kubectl get pod 同一套心智。

二、数据契约

deviation 对象

```json
{
  ”id“: ”dev_01J8X...“,
  ”created_at“: ”2026-10-18T09:12:03Z“,
  ”scene“: ”要求写代码却给了大段铺陈“,
  ”expected“: ”三行以内的可运行代码“,
  ”actual“: ”五段解释加伪代码“,
  ”gap“: ”我默认结论优先，它按全面覆盖来写“,
  ”prompt“: ”刚才你的回答偏在铺陈展开……“,
  ”rule_id“: null
}
```

rule 对象

```json
{
  ”id“: ”rule_01J8Y...“,
  ”created_at“: ”2026-10-18T09:20:00Z“,
  ”text“: ”先结论后细节，除非我明确要展开“,
  ”source_ids“: [”dev_01J8X...“, ”dev_01J8Z...“]
}
```

三、输入侧：位置参数 + —stdin

简单字段走 flag，复杂结构走 stdin，两者可混用（stdin 优先）：

```bash
# 人用
collab deviation log \
  —scene ”要求写代码却给了大段铺陈“ \
  —expected ”三行以内的可运行代码“ \
  —actual ”五段解释加伪代码“ \
  —gap ”我默认结论优先，它按全面覆盖来写“ \
  —prompt ”刚才你的回答偏在铺陈展开……“

# 模型用：整条 JSON 从 stdin 进，字段名和输出一致
echo ’{”scene“:”...“,”expected“:”...“,”actual“:”...“,”gap“:”...“,”prompt“:”...“}‘ \
  | collab deviation log —stdin
```

幂等：log 用 sha256(scene + expected + actual + gap) 去重。重复提交不报错，返回已有记录并标 ”deduplicated“: true，退出码 0。这样模型重试安全。

四、输出侧：默认人读，—json 给机器

```bash
collab deviation similar —scene ”写太多“ —json
```

```json
{
  ”matches“: [
    { ”id“: ”dev_01J8X...“, ”score“: 0.82, ”scene“: ”...“, ”gap“: ”...“ }
  ]
}
```

规则：

· —json 输出是稳定契约，字段只增不删，版本在 schema 里标。
· 错误一律写 stderr，也是 JSON：

```json
{”error“:{”code“:”NOT_FOUND“,”message“:”rule_01J8 不存在“,”hint“:”用 collab rule list 查看“}}
```

· 退出码语义固定：

码 含义
0 成功（含幂等去重）
2 参数/用法错误
3 未找到
4 冲突（如同一偏差提升到不同规则）
5 server 不可达

五、自描述：collab schema

```bash
collab schema                 # 全部命令的 schema 总表
collab schema deviation.log   # 单命令入参/出参 JSON Schema
```

这一条是整个设计的关键：这份 schema 就是未来 MCP tool 定义的同一份东西。加 MCP 适配时，deviation.log 的 schema 原样注册成 tool，不用重写。

六、核心命令的行为细节

deviation similar —— 第一版不做向量检索，简单打分：scene 子串/分词重合 + gap 关键词重合，返回按 score 排序的 top N（默认 5）。够用，可解释。

rule candidates —— 按 scene 归一化（小写、去标点、去空白）分组，count ≥ 2 的组返回：

```json
{
  ”candidates“: [
    { ”scene_key“: ”要求写代码却给了大段铺陈“, ”count“: 2, ”deviation_ids“: [”...“,”...“] }
  ]
}
```

rule promote —— 必须显式指定来源，且规则文本由用户/模型提供，工具不自动生成。这是守住「规则由用户点头才落库」：

```bash
collab rule promote —deviation dev_01J8X,dev_01J8Z —text ”先结论后细节，除非我明确要展开“
```

成功后回写这些 deviation 的 rule_id。

七、/停一下 这个 skill 怎么调它

skill 本身只是一段提示词流程，落地的调用就三行：

```bash
collab deviation similar —scene ”$SCENE“ —json        # 1. 有没有同类
collab deviation log —stdin <<< ”$RECORD_JSON“          # 2. 记这次
collab rule candidates —json                            # 3. 够不够格立规则
```

模型在 shell 里跑这三条，和它跑 gh pr view —json 没有任何区别——这就是前面说的「AI 原生的 CLI」。

八、MVP 范围与不做的事

第一版做：上面 8 个命令、SQLite 本地存储、HTTP server 单进程、—json + schema + 结构化错误、幂等。

第一版不做：向量检索、多用户、同步、MCP 适配、自动提炼规则文本、被动触发。这些都在契约稳定之后再加，且都只是同一层薄封装。

九、落地建议

1. 先写 API 契约（4 个 endpoint：POST /deviations、GET /deviations/similar、GET /rules/candidates、POST /rules），用 OpenAPI 或手写 schema；
2. server 用 SQLite 起一版，跑通「log → similar → candidates → promote」这条链；
3. CLI 做薄客户端，—json 直接透传 server 响应，不做二次加工；
4. skill 里写死那三条命令，跑两周，看用户是否真的会粘回生成的 prompt。

这样第一版就是一个能自证的小闭环：不依赖 MCP、不依赖特定客户端、人和模型都能用，而且每一层都为后面的扩展留好了缝。
