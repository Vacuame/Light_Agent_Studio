# 质量门索引

质量门是关键产物交接、回报或关闭前的检查点。

它不检查“角色本人”，而是检查“产物能不能交给下一环节、向上回报或支持关闭任务”。

## 读取原则

角色只需要读取自己当前任务相关的质量门，不需要读取所有质量门。

例如：

- Architect 只读 `rules/gates/architecture-gate.md`
- Developer 只读 `rules/gates/development-gate.md`
- Tester 只读 `rules/gates/test-gate.md`

如果当前任务使用了子任务、并行任务或任务级 handoff/report，对应质量门只检查当前任务相关的交接、回报和风险是否清楚，不强制固定任务层级。

## 质量门列表

| 质量门 | 适用场景 | 文件 |
|---|---|---|
| 管理门 | 修改规则、角色、技能、项目配置、任务状态结构前 | `rules/gates/administration-gate.md` |
| 架构门 | 架构设计交给模块设计、子任务或上层回报前 | `rules/gates/architecture-gate.md` |
| 模块门 | 模块设计交给开发、子任务或上层回报前 | `rules/gates/module-gate.md` |
| 开发门 | 代码交给测试、子任务或上层回报前 | `rules/gates/development-gate.md` |
| 测试门 | 测试结果支持任务回报或关闭前 | `rules/gates/test-gate.md` |
| 顾问产物门 | Adviser 写入供其他 Agent 阅读的文件前 | `rules/gates/adviser-output-gate.md` |

## 结论格式

所有质量门统一使用以下结论：

```text
PASS：可以交接、回报、关闭或修改
CONCERNS：可以继续，但必须记录风险
BLOCKED：不能继续，必须先补充或修正
```

## 与任务目录的关系

- 向下交接前，检查对应任务目录的 `handoff.md` 是否清楚。
- 向上回报前，检查对应任务目录的 `report.md` 是否清楚。
- 任务关闭前，检查任务状态、风险、未完成项和必要的子任务回报。
- 如果任务没有交接，不强制创建 `handoff.md`。
- 闭环时必须有 `report.md`。
