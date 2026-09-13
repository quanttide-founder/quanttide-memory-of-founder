# 智能体

一种新的架构思路：默认偏移模型做，规则引擎判断，结果差就找上级模型修正。

这需要对模型能力有充分理解，而且有合适的规则可以调度。

具体可以使用不同维度的测评分数为基准，同时结合自定义的维度和测评迭代。

聪明模型要限制，而且要对比聪明模型和笨蛋模型积累经验进化。

高风险任务要人类二次核验。

伪代码示例：

out = l0.run(task)
signals = rules.score(task, out)

if signals.risk == ”high“ or not signals.schema_valid or signals.confidence < τ_low:
    out = l1.correct(task, out, signals)
    log.write(task, out0=out, signals=signals, corrected=out)
    budget.consume()
elif signals.confidence < τ_mid and budget.left() > 0:
    out = l1.review(task, out, signals)
    log.write(...)

