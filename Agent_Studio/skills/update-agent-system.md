# Skill: update-agent-system

用于修改 Agent 架构本身。

## 主要角色

- Administrator

## 适用场景

- 修改规则
- 修改角色
- 修改技能
- 修改质量门
- 修改项目配置
- 修改状态层结构
- 修改任务目录、handoff/report 协议、归档/删除规则

## 流程

1. 明确要修改什么。
2. 说明为什么要修改。
3. 分析影响范围。
4. 检查是否需要同步修改其他文件。
5. 如果修改状态结构，说明旧状态文件如何迁移、删除或归档。
6. 如果会删除任务目录或状态文件，获得用户明确确认。
7. 读取 `rules/gates/administration-gate.md`，通过管理门。
8. 用户确认。
9. 修改文件。
10. 记录变更。
11. 更新 `state/active.md`、`state/tasks/index.md` 或当前任务目录状态。

## 输出

- 更新后的规则、角色或技能文件
- 必要时写入 `docs/decisions/`
- `state/active.md`
- `state/tasks/index.md`
- 当前任务目录下的 `progress.md` 或 `report.md`

## 禁止

- 不允许无影响分析直接改规则。
- 不允许绕过用户确认。
- 不允许未确认就删除任务目录。
- 不允许只改单个文件而留下旧状态路径引用。
