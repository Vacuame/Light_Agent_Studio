# Skill: module-design

用于把架构或需求拆成具体模块设计。

## 目标

- 写清模块目标
- 写清输入输出
- 写清接口
- 写清数据流
- 写清实现落点
- 写清边界情况
- 写清验收标准
- 必要时写Agent 工作区 handoff 或 report

## 常见执行角色

- Module Designer

## 权限

本 skill 不授予额外权限；执行者必须遵守当前角色文件中的权限边界。

## 任务输入

本 skill 按任务需要使用：

- `docs/project-overview.md`
- `docs/architecture.md`
- `docs/module-map.md`
- 相关 `docs/decisions/`
- 项目源码和目录结构，仅用于定位已有职责归属
- `rules/gates/module-gate.md`
- `skills/templates/module-template.md`：用户要求起草模块设计文档时按需使用。

状态层读取规则见 `rules/context-rules.md`。

## 流程

1. 定位当前顶层任务目录和 Agent 工作区。
2. 明确要设计哪个模块或工作单元。
3. 读取架构和模块地图。
4. 判断模块边界和依赖。
5. 读取相关源码入口和项目结构，定位现有职责 owner。
6. 向用户确认不清楚的点。
7. 起草模块设计，必须包含 `实现落点`。
8. 读取 `rules/gates/module-gate.md`，通过模块门检查。
9. 用户确认后写入 `docs/modules/<module-name>.md`。
10. 需要交接或回报时，按 `skills/handoff.md` 执行。

任务是否拆分、拆几个子任务、由哪些角色接手，由用户或当前任务 owner 决定。本 skill 不强制创建实现子任务。

## 角色边界

角色权限边界见当前 `agents/<role>.md`。本 skill 只定义模块设计流程，不扩大执行者权限。

如果无法确定实现落点，必须标为 `待确认`，不得编造路径、类名、函数名或接口名。

## 输出

- `docs/modules/<module-name>.md`（用户确认后）
- 当前 Agent 工作区的 `report.md`（用户明确要求或确认后）
- 接手或下游 Agent 工作区的 `handoff.md`（用户明确要求或确认后）
- `state/<task-id>/overview.md`（父级、汇总者或任务 owner 需要整理稳定任务级结论，且用户确认后）
