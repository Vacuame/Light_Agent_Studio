# Skill: implement

用于根据模块设计实现代码。

## 目标

- 按模块设计写代码
- 记录实现说明
- 标记偏离设计的地方
- 给 Tester 提供测试交接

## 主要角色

- Developer

## 必读文件

- 对应 `docs/modules/<module-name>.md`
- `docs/architecture.md`
- 相关 `docs/decisions/`
- `rules/project-config.md`
- `state/handoff.md`

## 流程

1. 读取模块设计和交接说明。
2. 检查是否有不清楚的设计点。
3. 给出实现计划。
4. 用户确认。
5. 实现代码。
6. 记录实现说明和变更。
7. 读取 `rules/gates/development-gate.md`，通过开发门检查。
8. 写交接给 Tester。

## 启动条件

只有当前窗口角色是 Developer，或用户明确要求“切换到 Developer 并开始实现”时，才能使用本 skill 修改项目代码。

如果当前窗口是 Architect、Module Designer，或“架构+模块”组合角色，应停止并回到模块设计或 handoff，不得调用本 skill。

## 输出

- 代码
- `docs/implementation/change-log.md`
- `state/handoff.md`

## 禁止

- 不擅自改架构。
- 不擅自引入依赖。
- 不擅自改变模块目标。
