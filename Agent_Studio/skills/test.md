# Skill: test

用于制定测试计划、执行测试、记录结果。

## 目标

- 根据模块验收标准测试
- 记录测试结果
- 记录 bug
- 判断当前测试对象是否可以回报或关闭

## 主要角色

- Tester

## 必读文件

- 对应 `docs/modules/<module-name>.md`
- `docs/implementation/change-log.md`
- `rules/project-config.md`
- `state/tasks/<task-id>/overview.md`
- 当前顶层任务的 `overview.md` 和当前 Agent 工作区的 `handoff.md` / `report.md`
- 当前 Agent 工作区的 `handoff.md`（如果存在）
- 当前 Agent 工作区的 `report.md`（如果存在）

## 流程

1. 定位当前顶层任务目录和 Agent 工作区。
2. 读取模块设计和实现交接。
3. 提取验收标准。
4. 制定测试计划。
5. 用户确认测试范围。
6. 执行测试或说明需要用户手动执行的测试。
7. 写测试报告。
8. 记录 bug。
9. 读取 `rules/gates/test-gate.md`，通过测试门判断当前测试对象是否可以回报或关闭。
10. 如果需要向上层、owner 或用户留下测试结论，写当前 Agent 工作区的 `report.md`，说明测试结论、风险、是否建议关闭。
11. 如需交给其他角色继续处理，写接手 Agent 工作区的 `handoff.md`。
12. 父级、汇总者或任务 owner 读取 report 后，决定是否更新顶层任务 `overview.md`。

## 输出

- `docs/tests/test-plan.md`（用户确认后）
- `docs/tests/test-report.md`（用户确认后）
- `docs/tests/bug-list.md`（用户确认后）
- 当前 Agent 工作区的 `report.md`（需要向上回报时）
- 接手或下游 Agent 工作区的 `handoff.md`（需要交接时）
- `state/tasks/<task-id>/overview.md`（父级、汇总者或任务 owner 需要整理稳定任务级结论时）
