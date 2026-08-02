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
- `state/active.md`
- `state/tasks/index.md`
- 当前任务目录下的 `meta.md`、`progress.md`
- 当前任务目录下的 `handoff.md`（如果存在）
- 当前任务目录下的 `links.md`、`report.md`（如果存在）

## 流程

1. 定位当前任务目录。
2. 读取模块设计和实现交接。
3. 提取验收标准。
4. 制定测试计划。
5. 用户确认测试范围。
6. 执行测试或说明需要用户手动执行的测试。
7. 写测试报告。
8. 记录 bug。
9. 读取 `rules/gates/test-gate.md`，通过测试门判断当前测试对象是否可以回报或关闭。
10. 更新当前任务目录的 `progress.md`。
11. 写当前任务目录的 `report.md`，说明测试结论、风险、是否可以关闭。
12. 如需交给其他角色继续处理，写对应任务目录的 `handoff.md`。
13. 更新 `state/active.md` 和 `state/tasks/index.md`。

## 输出

- `docs/tests/test-plan.md`
- `docs/tests/test-report.md`
- `docs/tests/bug-list.md`
- 当前任务目录下的 `progress.md`
- 当前任务目录下的 `report.md`
- 必要时：当前任务或子任务目录下的 `handoff.md`
- `state/active.md`
- `state/tasks/index.md`
