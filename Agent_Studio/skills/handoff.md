# Skill: handoff

用于在 Agent 之间写交接和回报。

## 目标

- 让下级、下游或接手者知道如何继续
- 让上级、上层汇总者、任务 owner 或用户知道当前结果、阻塞、风险或需要判断的问题
- 避免多个 Agent 覆盖同一个交流文件
- 区分状态层交流文件和正式产物

## 核心概念

`handoff.md` 和 `report.md` 只是工作交流文件，不是状态机、流程引擎或阶段判定器。

```text
handoff.md = 写给下级、下游或接手者
report.md  = 写给上级、上层汇总者、任务 owner 或用户
```

写入位置：

```text
handoff.md 写在接手者 Agent 工作区。
report.md  写在当前 Agent 自己的工作区。
```

顶层任务目录 `state/tasks/<task-id>/` 不是 Agent 工作区，不直接放 `handoff.md` 或 `report.md`。

## 必读文件

- `state/tasks/<task-id>/overview.md`
- 当前 Agent 工作区的 `handoff.md`（如果存在）
- 当前 Agent 工作区的 `report.md`（如果存在）
- 必要的父级、子级或兄弟工作区 `report.md`
- 当前任务相关产物

如果要给下游写交接，先确认接手者工作区。

如果要向上回报，先确认当前 Agent 工作区和回报对象。

## 流程：向下交接

需要下级、下游或接手者继续工作时：

1. 明确交接给谁。
2. 明确接手什么。
3. 定位或创建接手者 Agent 工作区。
4. 在接手者 Agent 工作区写 `handoff.md`。

`handoff.md` 应写清楚：

- 交接来源
- 交接给谁
- 接手什么
- 必读文件
- 已确认内容
- 临时假设
- 风险
- 下一步建议

如果交给 Developer，还应写清楚实现落点摘要。

写 `handoff.md` 不代表当前工作区自动结束，不自动要求写当前工作区 `report.md`，也不自动更新 `overview.md`。

## 流程：向上回报

需要向父级、上层汇总者、任务 owner 或用户说明当前结果、阻塞、风险或请求判断时：

1. 明确回报给谁。
2. 明确本次回报说明什么。
3. 在当前 Agent 工作区写 `report.md`。

`report.md` 应写清楚：

- 回报给谁
- 本工作区结论：PASS / CONCERNS / BLOCKED / DROPPED
- 完成内容
- 修改或产出文件
- 验证结果
- 未完成项
- 风险与注意事项
- 对上层任务的影响
- 建议下一步

`report.md` 只表达当前工作区的回报内容，不代表顶层任务自动完成，不自动要求更新 `overview.md`。

## 任务创建

如果用户或任务 owner 要开启新的顶层任务：

1. 创建 `state/tasks/<task-id>/`。
2. 创建或更新 `overview.md`，记录任务目标、背景、当前状态和重要关系。
3. 如果已有明确接手 Agent，创建对应 Agent 工作区。
4. 如果需要交给接手 Agent，在接手者工作区写 `handoff.md`。

不要在顶层任务目录直接创建 `handoff.md` 或 `report.md`。

## 输出

按实际交流需要输出：

- `state/tasks/<task-id>/<receiver-agent-workspace>/handoff.md`
- `state/tasks/<task-id>/<current-agent-workspace>/report.md`
- `state/tasks/<task-id>/<agent-workspace>/<child-agent-workspace>/handoff.md`
- `state/tasks/<task-id>/<agent-workspace>/<child-agent-workspace>/report.md`
- `state/tasks/<task-id>/overview.md`（只有任务 owner、父级或汇总者需要整理稳定任务级结论时）

## 禁止

- 不在顶层任务目录直接写 `handoff.md`。
- 不在顶层任务目录直接写 `report.md`。
- 不把 `handoff.md` 当成完成报告。
- 不把 `report.md` 当成顶层任务完成证明。
- 不因为写了 `handoff.md` 就自动写 `report.md`。
- 不因为写了 `report.md` 就自动更新 `overview.md`。
- 不把临时状态写入全局 `docs/`。
