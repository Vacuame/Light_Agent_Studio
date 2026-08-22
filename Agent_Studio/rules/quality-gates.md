# 质量门索引

质量门是关键产物准备交接、准备向上留痕、或准备支持关闭判断前的检查点。

它不检查“角色本人”，而是检查“产物能不能交给下一环节、向上回报或支持关闭任务”。

## 读取原则

角色只需要读取自己当前交付物相关的质量门，不需要读取所有质量门。

质量门不授予额外权限；执行者仍必须遵守当前角色文件、`rules/rules.md` 和 `rules/project-config.md`。

## 证据充分性

质量门除检查"是否清楚"外，还必须检查承载下游决策的事实类结论是否满足 `rules/rules.md` 结论纪律：有确定性标注和依据，否定性结论有排除范围。无依据的结论不能交接、回报或支持关闭。

## 质量门列表

| 质量门 | 适用交付物 | 文件 |
|---|---|---|
| 管理门 | 规则、角色、技能、质量门、项目配置、状态结构变更 | `rules/gates/administration-gate.md` |
| 架构门 | 架构设计、架构交接、架构阶段回报 | `rules/gates/architecture-gate.md` |
| 模块门 | 模块设计、模块实现交接、模块阶段回报 | `rules/gates/module-gate.md` |
| 开发门 | 代码实现、测试交接、实现阶段回报 | `rules/gates/development-gate.md` |
| 测试门 | 测试计划、测试结果、bug 记录、关闭建议 | `rules/gates/test-gate.md` |
| 顾问产物门 | Adviser 写给其他 Agent 阅读的辅助材料 | `rules/gates/adviser-output-gate.md` |

## 结论格式

所有质量门统一使用以下结论：

```text
PASS：可以交接、回报、关闭或修改
CONCERNS：可以继续，但必须记录风险
BLOCKED：不能继续，必须先补充或修正
```

## 与任务目录的关系

质量门只检查交付物是否清楚，不强制创建状态层交流文件。

- 如果需要向下交接，按 `rules/collaboration-rules.md` 的确认机制写 `handoff.md`，并检查其内容是否清楚。
- 如果需要向上留痕，按 `rules/collaboration-rules.md` 的确认机制写 `report.md`，并检查其内容是否清楚。
- 如果任务没有交接，不强制创建 `handoff.md`。
- 如果不需要向上级、owner 或用户留痕，不强制创建 `report.md`。
