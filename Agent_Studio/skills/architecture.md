# Skill: architecture

用于进行总体架构设计。

## 目标

- 明确项目整体结构
- 划分模块边界
- 确定技术路线
- 记录重要技术决策
- 必要时写Agent 工作区 handoff 或 report

## 常见执行角色

- Architect

## 权限

本 skill 不授予额外权限。执行者必须遵守当前角色文件、`rules/rules.md` 和 `rules/project-config.md` 的权限边界。

状态层结构和文件格式见 `rules/context-rules.md`；handoff/report 写入方向、位置和确认机制见 `rules/collaboration-rules.md`。

## 必读文件

在 `rules/rules.md` 的通用必读基线之外，本 skill 按任务需要读取：

- `docs/project-overview.md`
- `docs/architecture.md`
- `docs/module-map.md`
- `docs/decisions/`
- `rules/gates/architecture-gate.md`

状态层读取规则见 `rules/context-rules.md`。

## 流程

1. 定位当前顶层任务目录和 Agent 工作区。
2. 读取项目背景和现有架构。
3. 识别目标、约束、风险。
4. 提出 2-3 个架构方案或调整方案。
5. 用户选择。
6. 起草架构更新。
7. 读取 `rules/gates/architecture-gate.md`，通过架构门检查。
8. 用户确认后更新正式产物。
9. 如果需要向上层、owner 或用户留下阶段结论，先说明拟写 report 摘要并询问是否写入；用户确认后写当前 Agent 工作区的 `report.md`。
10. 如果需要交给下游 Agent 或角色，先说明接手对象和 handoff 摘要并询问是否写入；用户确认后写接手 Agent 工作区的 `handoff.md`。
11. 父级、汇总者或任务 owner 读取 report 后，决定是否更新顶层任务 `overview.md`。

任务是否拆分、拆几个子任务、由哪些角色接手，由用户或当前任务 owner 决定。本 skill 不强制创建模块子任务。

## 角色边界

角色权限边界见当前 `agents/<role>.md`。本 skill 只定义架构设计流程，不扩大执行者权限。

## 输出

- `docs/architecture.md`（用户确认后）
- `docs/module-map.md`（用户确认后）
- `docs/decisions/decision-xxx.md`（用户确认后）
- 当前 Agent 工作区的 `report.md`（用户明确要求或确认后）
- 接手或下游 Agent 工作区的 `handoff.md`（用户明确要求或确认后）
- `state/tasks/<task-id>/overview.md`（父级、汇总者或任务 owner 需要整理稳定任务级结论，且用户确认后）
