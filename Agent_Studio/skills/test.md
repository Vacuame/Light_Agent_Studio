# Skill: test

用于制定测试计划、执行测试、记录结果。

## 目标

- 根据模块验收标准测试
- 记录测试结果
- 记录 bug
- 判断当前测试对象是否可以回报或关闭

## 常见执行角色

- Tester

## 权限

本 skill 不授予额外权限；执行者必须遵守当前角色文件中的权限边界。

## 任务输入

本 skill 按任务需要使用：

- 对应 `docs/modules/<module-name>.md`
- `docs/implementation/change-log.md`
- `docs/project-config.md`（如存在）
- `rules/gates/test-gate.md`

状态层读取规则见 `rules/context-rules.md`。

## 流程

1. 定位当前顶层任务目录和 Agent 工作区。
2. 读取模块设计和实现交接。
3. 提取验收标准。
4. 制定测试计划。
5. 用户确认测试范围。
6. 执行测试或说明需要用户手动执行的测试。
7. 在对话中汇总测试结果。
8. 如果需要写入 `docs/tests/*`、`report.md`、`handoff.md` 或 bug 记录，先说明拟写摘要并询问用户是否写入。
9. 读取 `rules/gates/test-gate.md`，通过测试门判断当前测试对象是否可以回报或建议关闭。
10. 需要交接或回报时，按 `skills/handoff.md` 执行。

## 输出

- `docs/tests/test-plan.md`（用户确认后）
- `docs/tests/test-report.md`（用户确认后）
- `docs/tests/bug-list.md`（用户确认后）
- 当前 Agent 工作区的 `report.md`（用户明确要求或确认后）
- 接手或下游 Agent 工作区的 `handoff.md`（用户明确要求或确认后）
- `state/<task-id>/overview.md`（父级、汇总者或任务 owner 需要整理稳定任务级结论，且用户确认后）
