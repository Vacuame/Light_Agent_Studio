# Skill: architecture

用于进行总体架构设计。

## 目标

- 明确项目整体结构
- 划分模块边界
- 确定技术路线
- 记录重要技术决策
- 必要时写任务级 handoff 或 report

## 主要角色

- Architect

## 必读文件

- `docs/project-overview.md`
- `docs/architecture.md`
- `docs/module-map.md`
- `docs/decisions/`
- `rules/project-config.md`
- `state/active.md`
- `state/tasks/index.md`
- 当前任务目录下的 `meta.md`、`progress.md`
- 当前任务目录下的 `handoff.md`、`report.md`、`links.md`（如果存在）

## 流程

1. 定位当前任务目录。
2. 读取项目背景和现有架构。
3. 识别目标、约束、风险。
4. 提出 2-3 个架构方案或调整方案。
5. 用户选择。
6. 起草架构更新。
7. 读取 `rules/gates/architecture-gate.md`，通过架构门检查。
8. 用户确认后更新正式产物。
9. 更新当前任务目录的 `progress.md`。
10. 如果需要交给下游任务或角色，写对应任务目录的 `handoff.md`。
11. 如果架构任务阶段结束或需要向上层/用户回报，写当前任务目录的 `report.md`。
12. 更新 `state/active.md` 和 `state/tasks/index.md`。

任务是否拆分、拆几个子任务、由哪些角色接手，由用户或当前任务 owner 决定。本 skill 不强制创建模块子任务。

## 角色边界

- 本 skill 不允许修改项目代码、配置、资源、测试代码或构建脚本。
- 本 skill 不允许运行用于验证代码改动的构建或测试。
- 如果用户提出具体功能，只能输出架构方案、影响范围和交接建议。
- 需要实现时，必须请求用户明确切换到 Developer。

## 输出

- `docs/architecture.md`
- `docs/module-map.md`
- `docs/decisions/decision-xxx.md`
- 当前任务目录下的 `progress.md`
- 必要时：当前任务或子任务目录下的 `handoff.md`
- 必要时：当前任务目录下的 `report.md`
- `state/active.md`
- `state/tasks/index.md`
