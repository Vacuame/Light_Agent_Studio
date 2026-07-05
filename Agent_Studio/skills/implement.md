# Skill: implement

用于根据模块设计实现代码。

## 目标

- 按模块设计写代码
- 遵守模块设计中的实现落点
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
2. 检查模块设计和交接说明是否包含实现落点。
3. 对照真实代码验证实现落点是否可行。
4. 检查新增 API 的归属层级，避免基础类、系统类或 Manager 类门面膨胀。
5. 检查是否有不清楚的设计点。
6. 给出实现计划，必须包含层级边界说明。
7. 用户确认。
8. 实现代码。
9. 记录实现说明和变更。
10. 读取 `rules/gates/development-gate.md`，通过开发门检查。
11. 写交接给 Tester。

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
- 不在实现落点缺失或冲突时自行决定代码层级。
- 不静默偏离模块设计中的实现落点。
- 不为了调用方便向基础类、系统类或 Manager 类添加具体功能门面方法。
- 不把具体能力塞进所有对象共有的基类；优先使用组件、接口、专门服务或明确的模块 owner。
- 如果必须修改基础类、系统类或 Manager 类 API，先说明原因并等待用户确认。
