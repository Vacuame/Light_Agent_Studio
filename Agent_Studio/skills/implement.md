# Skill: implement

用于根据模块设计实现代码。

## 目标

- 按模块设计写代码
- 核实并执行模块设计与交接中的实现落点，以真实代码为准
- 记录实现说明
- 记录落点或方案偏离交接与设计的地方及原因
- 给 Tester 提供测试交接，或向上层回报实现结果

## 常见执行角色

- Developer

## 权限

本 skill 不授予额外权限；执行者必须遵守当前角色文件中的权限边界。

## 任务输入

本 skill 按任务需要使用：

- 对应 `docs/modules/<module-name>.md`
- `docs/architecture.md`
- 相关 `docs/decisions/`
- `docs/project-config.md`（如存在）
- `rules/gates/development-gate.md`

状态层读取规则见 `rules/context-rules.md`。

## 流程

1. 定位当前顶层任务目录和 Agent 工作区。
2. 读取模块设计和 Agent 工作区交接说明。交接内容的信任等级按 `rules/collaboration-rules.md` 执行：事实断言默认待核实，实现落点是建议，边界约束仍有效。
3. 检查模块设计和交接说明是否包含实现落点。
4. 对照真实代码验证实现落点是否可行：不只核实位置存在，还必须核实落点与既有系统机制的兼容性——同类内容现在如何运作、本次改动从写入到生效会经过哪些既有步骤。发现交接或设计中的事实断言、落点与真实代码不符时，以事实为准并反馈上游或用户，不得在错误前提上叠补丁实现。
5. 检查新增 API 的归属层级，避免基础类、系统类或 Manager 类门面膨胀。
6. 检查是否有不清楚的设计点。
7. 给出实现计划，必须包含层级边界说明。
8. 用户确认。
9. 实现代码。
10. 在对话中说明实现完成、修改文件、验证结果、偏离与原因、风险和下一步建议。
11. 读取 `rules/gates/development-gate.md`，通过开发门检查。
12. 需要交接或回报时，按 `skills/handoff.md` 执行。

## 启动条件

只有当前窗口角色是 Developer，或用户明确要求“切换到 Developer 并开始实现”时，才能使用本 skill 修改项目代码。

如果当前角色无权实现，应停止并回到当前角色允许的设计、交接或确认流程，不得调用本 skill。

## 输出

- 代码
- `docs/implementation/change-log.md`（用户确认后）
- 当前 Agent 工作区的 `report.md`（用户明确要求或确认后）
- 接手或下游 Agent 工作区的 `handoff.md`（用户明确要求或确认后）
- `state/<task-id>/overview.md`（父级、汇总者或任务 owner 需要整理稳定任务级结论，且用户确认后）

## 禁止

实现相关权限边界见当前 `agents/<role>.md`。本 skill 只定义实现流程，不授予偏离架构、引入依赖、改变模块边界或扩大基础类/系统类/Manager API 的权限。
