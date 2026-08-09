# Skill: handoff

用于任务交接、任务回报、任务创建、任务关闭和会话结束前整理。

## 目标

- 防止断片
- 告诉下一个角色或子任务从哪里继续
- 告诉上层任务或用户当前任务结果
- 区分临时状态和正式产物
- 避免多个任务或多个 Agent 覆盖同一个交接文件

## 核心概念

```text
handoff.md = 向下交接
report.md  = 向上回报
```

所有交接和回报都写入对应 Agent 工作区。

## 必读文件

- `state/tasks/<task-id>/overview.md`
- 当前顶层任务的 `overview.md`
- 当前 Agent 工作区的 `report.md`
- 当前任务相关产物

如果要接手已有交接，读取当前 Agent 工作区的 `handoff.md`。

如果要汇总子任务或关闭任务，读取相关子任务的 `report.md`。

## 流程：创建任务或子任务

1. 明确任务目标。
2. 明确任务 owner 或接手角色。
3. 创建任务目录：`state/tasks/<task-id>/`。
4. 写 `overview.md`。
5. 写 `report.md`。
6. 必要时写 `handoff.md`。
7. 必要时写 `相关工作区 report`。
8. 更新顶层任务 `overview.md`。
9. 更新 `state/tasks/<task-id>/overview.md`。

任务如何拆分由用户或当前任务 owner 决定。本 skill 不判断任务是大、中、小，也不强制创建子任务。

## 流程：向下交接

1. 明确交接给谁。
2. 明确接手什么。
3. 列出必读文件。
4. 列出已确认内容。
5. 列出临时假设。
6. 列出风险。
7. 如果交给 Developer，列出实现落点摘要。
8. 列出下一步。
9. 写入接手任务目录的 `handoff.md`。
10. 更新接手任务的 `overview.md` 和 `report.md`。
11. 更新顶层任务 `overview.md`。

## 流程：向上回报

1. 总结当前任务。
2. 列出已完成内容。
3. 列出修改或产出文件。
4. 列出验证结果。
5. 列出未完成内容。
6. 列出风险与注意事项。
7. 说明对上层任务的影响。
8. 给出建议下一步。
9. 写入当前顶层任务目录和 Agent 工作区的 `report.md`。
10. 更新当前任务的 `overview.md` 和 `report.md`。
11. 更新顶层任务 `overview.md`。

## 流程：关闭任务

1. 读取当前任务的 `report.md`。
2. 如果有子任务，读取必要子任务的 `report.md`。
3. 检查是否通过相关质量门。
4. 检查是否存在未解决风险或 CONCERNS。
5. 用户确认关闭后，标记任务为 `done` 或 `dropped`。
6. 更新顶层任务 `overview.md`。

## 流程：完成记录任务

1. 确认任务状态为 `done` 或 `dropped`。
2. 确认用户同意完成记录。
3. 在任务目录写或更新 `overview.md`。
4. 将任务目录移动到 `state/tasks/<task-id>/（完成后不默认移动）`。
5. 更新顶层任务 `overview.md`。
6. 更新 `state/tasks/<task-id>/overview.md`。

## 流程：删除任务

删除任务目录是破坏性操作，必须先获得用户明确确认。

1. 确认任务状态为 `done` 或 `dropped`。
2. 确认任务没有需要保留的长期价值。
3. 如果有子任务，先处理子任务。
4. 用户确认后删除任务目录。
5. 更新顶层任务 `overview.md`。
6. 更新 `state/tasks/<task-id>/overview.md`。

## 输出

按场景输出：

- `state/tasks/<task-id>/overview.md`
- `state/tasks/<task-id>/report.md`
- `state/tasks/<task-id>/handoff.md`
- `state/tasks/<task-id>/report.md`
- `state/tasks/<task-id>/相关工作区 report`
- `state/tasks/<task-id>/overview.md`

## 禁止

- 交接只写对应 Agent 工作区的 `handoff.md`。
- 不替用户判断任务必须拆成大、中、小结构。
- 不在没有用户确认时删除任务目录。
- 不把临时状态写入 `docs/`。
- 不把 `handoff.md` 当成完成报告；完成或阶段结论写 `report.md`。
