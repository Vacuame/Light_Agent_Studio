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

## 主要角色

- Module Designer

## 必读文件

- `docs/project-overview.md`
- `docs/architecture.md`
- `docs/module-map.md`
- 相关 `docs/decisions/`
- 项目源码和目录结构，仅用于定位已有职责归属
- `state/tasks/<task-id>/overview.md`
- 当前顶层任务的 `overview.md` 和当前 Agent 工作区的 `handoff.md` / `report.md`
- 当前 Agent 工作区的 `handoff.md`、`report.md`（如果存在）

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
10. 如果需要向上层、owner 或用户留下阶段结论，写当前 Agent 工作区的 `report.md`。
11. 如果需要交给 Developer 或其他下游 Agent，写接手 Agent 工作区的 `handoff.md`，必须包含实现落点摘要。
12. 父级、汇总者或任务 owner 读取 report 后，决定是否更新顶层任务 `overview.md`。

任务是否拆分、拆几个子任务、由哪些角色接手，由用户或当前任务 owner 决定。本 skill 不强制创建实现子任务。

## 角色边界

- 本 skill 不允许修改项目代码、配置、资源、测试代码或构建脚本。
- 本 skill 不允许运行用于验证代码改动的构建或测试。
- “功能很简单”不代表可以跳过模块设计直接实现。
- 需要实现时，必须请求用户明确切换到 Developer。
- 如果无法确定实现落点，必须标为 `待确认`，不得编造路径、类名、函数名或接口名。

## 输出

- `docs/modules/<module-name>.md`（用户确认后）
- 当前 Agent 工作区的 `report.md`（需要向上回报时）
- 接手或下游 Agent 工作区的 `handoff.md`（需要交接时）
- `state/tasks/<task-id>/overview.md`（父级、汇总者或任务 owner 需要整理稳定任务级结论时）
