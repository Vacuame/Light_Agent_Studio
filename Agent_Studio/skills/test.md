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

本 skill 不授予额外权限；执行者必须遵守当前角色文件和角色加载清单中的权限边界。

## 任务输入

本 skill 按任务需要使用：

- 对应 `docs/modules/<module-name>.md`
- `docs/implementation/change-log.md`
- `rules/project-config.md`
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
10. 如果需要向上层、owner 或用户留下测试结论，用户确认后写当前 Agent 工作区的 `report.md`，说明测试结论、风险、是否建议关闭。
11. 如需交给其他角色继续处理，用户确认后写接手 Agent 工作区的 `handoff.md`。
12. 父级、汇总者或任务 owner 读取 report 后，决定是否更新顶层任务 `overview.md`。

## 输出

- `docs/tests/test-plan.md`（用户确认后）
- `docs/tests/test-report.md`（用户确认后）
- `docs/tests/bug-list.md`（用户确认后）
- 当前 Agent 工作区的 `report.md`（用户明确要求或确认后）
- 接手或下游 Agent 工作区的 `handoff.md`（用户明确要求或确认后）
- `state/tasks/<task-id>/overview.md`（父级、汇总者或任务 owner 需要整理稳定任务级结论，且用户确认后）
