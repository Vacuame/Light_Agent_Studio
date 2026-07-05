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

## 主要角色

- Module Designer

## 必读文件

- `docs/project-overview.md`
- `docs/architecture.md`
- `docs/module-map.md`
- 相关 `docs/decisions/`
- 项目源码和目录结构，仅用于定位现有职责归属
- `state/active.md`

## 流程

1. 明确要设计哪个模块。
2. 读取架构和模块地图。
3. 判断模块边界和依赖。
4. 读取相关源码入口和项目结构，定位现有职责 owner。
5. 向用户确认不清楚的点。
6. 起草模块设计，必须包含 `实现落点`。
7. 读取 `rules/gates/module-gate.md`，通过模块门检查。
8. 用户确认后写入 `docs/modules/<module-name>.md`。
9. 写 `state/handoff.md` 给 Developer，必须包含实现落点摘要。

## 角色边界

- 本 skill 不允许修改项目代码、配置、资源、测试代码或构建脚本。
- 本 skill 不允许运行用于验证代码改动的构建或测试。
- “功能很简单”不代表可以跳过模块设计直接实现。
- 需要实现时，必须请求用户明确切换到 Developer。
- 如果无法确定实现落点，必须标为 `待确认`，不得编造路径、类名、函数名或接口名。

## 输出

- `docs/modules/<module-name>.md`
- `state/handoff.md`
