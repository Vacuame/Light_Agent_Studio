# Skill: architecture

用于进行总体架构设计。

## 目标

- 明确项目整体结构
- 划分模块边界
- 确定技术路线
- 记录重要技术决策

## 主要角色

- Architect

## 必读文件

- `docs/project-overview.md`
- `docs/architecture.md`
- `docs/module-map.md`
- `docs/decisions/`
- `rules/project-config.md`
- `state/active.md`

## 流程

1. 读取项目背景和现有架构。
2. 识别目标、约束、风险。
3. 提出 2-3 个架构方案或调整方案。
4. 用户选择。
5. 起草架构更新。
6. 读取 `rules/gates/architecture-gate.md`，通过架构门检查。
7. 用户确认后更新正式产物。
8. 更新 `state/active.md` 和必要的 `state/handoff.md`。

## 角色边界

- 本 skill 不允许修改项目代码、配置、资源、测试代码或构建脚本。
- 本 skill 不允许运行用于验证代码改动的构建或测试。
- 如果用户提出具体功能，只能输出架构方案、影响范围和交接建议。
- 需要实现时，必须请求用户明确切换到 Developer。

## 输出

- `docs/architecture.md`
- `docs/module-map.md`
- `docs/decisions/decision-xxx.md`
