# Skill: module-design

用于把架构或需求拆成具体模块设计。

## 目标

- 写清模块目标
- 写清输入输出
- 写清接口
- 写清数据流
- 写清边界情况
- 写清验收标准

## 主要角色

- Module Designer

## 必读文件

- `docs/project-overview.md`
- `docs/architecture.md`
- `docs/module-map.md`
- 相关 `docs/decisions/`
- `state/active.md`

## 流程

1. 明确要设计哪个模块。
2. 读取架构和模块地图。
3. 判断模块边界和依赖。
4. 向用户确认不清楚的点。
5. 起草模块设计。
6. 读取 `rules/gates/module-gate.md`，通过模块门检查。
7. 用户确认后写入 `docs/modules/<module-name>.md`。
8. 写 `state/handoff.md` 给 Developer。

## 输出

- `docs/modules/<module-name>.md`
- `state/handoff.md`
