# Skill: handoff

用于在用户明确要求执行交接或回报时，定位工作区、起草内容，并在确认后写入对应状态层交流文件。

## 目标

- 让下级、下游或接手者知道如何继续
- 让上级、上层汇总者、任务 owner 或用户知道当前结果、阻塞、风险或需要判断的问题
- 避免多个 Agent 覆盖同一个交流文件
- 区分状态层交流文件和正式产物

## 权限

本 skill 不授予额外权限；执行者必须遵守当前角色文件的职责和权限边界。

handoff/report 的方向、写入位置和确认机制见 `rules/collaboration-rules.md`；格式模板见 `rules/context-rules.md`。

## 授权预检查

`handoff.md` 和 `report.md` 属于状态层通信文件。创建或修改前必须有用户明确要求或确认。

它们不会因为以下事件自动创建或修改：

- 任务创建
- 阶段完成
- 实现完成
- 测试完成
- 会话压缩前整理
- 质量门通过
- 已经写了另一个 handoff/report

需要写入时，先在对话中说明：

- 写哪个文件
- 写给谁
- 为什么要写
- 拟写内容摘要

用户确认后再写入。

## 任务输入

本 skill 按任务需要使用：

- `state/tasks/<task-id>/overview.md`
- 当前 Agent 工作区的 `handoff.md`（如果存在）
- 当前 Agent 工作区的 `report.md`（如果存在）
- 必要的父级、子级或兄弟工作区 `report.md`
- 当前任务相关产物

如果要给下游写交接，先按 `rules/collaboration-rules.md` 判断接手者工作区应是当前工作区的子级、同级还是旁支。下游继续当前工作区范围内的工作时，默认使用当前工作区下的子工作区。

如果要向上回报，先确认当前 Agent 工作区和回报对象。

## 流程：向下交接

需要下级、下游或接手者继续工作时：

1. 明确交接给谁。
2. 明确接手什么。
3. 按 `rules/collaboration-rules.md` 判断接手者与当前工作区的关系：子级、同级或旁支。
4. 定位或创建接手者 Agent 工作区；如果是下游继续当前工作区范围内的工作，创建或使用当前工作区下的子工作区。
5. 按 `rules/collaboration-rules.md` 做交接前检查。
6. 说明拟写文件、写入原因和交接摘要，并询问用户是否写入。
7. 用户确认后，在接手者 Agent 工作区写 `handoff.md`。

`handoff.md` 推荐格式见 `rules/context-rules.md`。

起草 `handoff.md` 的“必读文件”时，只列当前交接任务的直接输入；不要复制通用 rules、角色文件、skill、质量门或项目配置清单。

## 流程：向上回报

需要向父级、上层汇总者、任务 owner 或用户说明当前结果、阻塞、风险或请求判断时：

1. 明确回报给谁。
2. 明确本次回报说明什么。
3. 按 `rules/collaboration-rules.md` 做回报前检查。
4. 说明拟写文件、写入原因和回报摘要，并询问用户是否写入。
5. 用户确认后，在当前 Agent 工作区写 `report.md`。

`report.md` 推荐格式见 `rules/context-rules.md`。

## 流程：任务创建

如果用户或任务 owner 要开启新的顶层任务：

1. 创建 `state/tasks/<task-id>/`。
2. 创建或更新 `overview.md`，记录任务目标、背景、当前状态和重要关系。
3. 如果已有明确接手 Agent，按 `rules/collaboration-rules.md` 判断接手工作区位置；没有当前父级工作区时，通常创建为顶层任务下的一级工作区。
4. 如果需要交给接手 Agent，先询问用户是否写 `handoff.md`，确认后在接手者工作区写入。

不要在顶层任务目录直接创建 `handoff.md` 或 `report.md`。

## 输出

按实际交流需要输出：

- 向子 Agent 交接：`state/tasks/<task-id>/<current-agent-workspace>/<child-agent-workspace>/handoff.md`（用户明确要求或确认后）
- 同级或旁支 Agent 交接：`state/tasks/<task-id>/<sibling-or-branch-workspace>/handoff.md`（用户明确要求或确认后）
- 当前 Agent 工作区的 `report.md`（用户明确要求或确认后）
- 顶层任务 `overview.md`（任务 owner、父级或汇总者需要整理稳定任务级结论，且用户确认后）

## 禁止

- 不在顶层任务目录直接写 `handoff.md`。
- 不在顶层任务目录直接写 `report.md`。
- 不把 `handoff.md` 当成完成报告。
- 不把 `report.md` 当成顶层任务完成证明。
- 不因为写了 `handoff.md` 就自动写 `report.md`。
- 不因为写了 `report.md` 就自动更新 `overview.md`。
- 不把临时状态写入全局 `docs/`。
