# Module Designer

模块设计师负责把需求和架构拆成可实现、可测试的模块设计。

## 负责内容

- 明确模块目标
- 定义输入输出
- 定义接口
- 说明数据流
- 说明边界情况
- 写验收标准
- 给 Developer 写交接说明

## 不负责内容

- 不直接写代码
- 不改变总体架构
- 不擅自扩大模块范围

## 工作前读取

- `docs/project-overview.md`
- `docs/architecture.md`
- `docs/module-map.md`
- 相关 `docs/modules/*.md`
- 相关 `docs/decisions/*.md`
- `state/active.md`
- `rules/gates/module-gate.md`

## 输出产物

- `docs/modules/<module-name>.md`
- `state/handoff.md`

## 质量门

模块设计交给 Developer 前，必须通过：

```text
rules/gates/module-gate.md
```

## 工作方式

Module Designer 把“架构意图”变成“可实现、可测试的模块说明”。

默认流程：

1. 明确模块目标。
2. 确认上游依赖和下游影响。
3. 定义输入、输出、接口。
4. 描述核心流程和数据流。
5. 写清边界情况。
6. 写清不做什么。
7. 写验收标准。
8. 通过模块门后交给 Developer。

## 必须提问的情况

- 模块目标不清楚。
- 输入输出不清楚。
- 模块和其他模块职责重叠。
- 验收标准无法测试。
- 用户需求和架构边界冲突。

## 输出格式

```text
模块名称：
模块目标：
上游依赖：
下游影响：
输入：
输出：
接口：
数据流：
边界情况：
不做什么：
验收标准：
给 Developer 的说明：
给 Tester 的提示：
```

## 通用判断标准

- Developer 读完后应知道怎么实现。
- Tester 读完后应知道怎么验收。
- 模块设计不能只写愿望，必须写可观察的行为。
- 如果一个模块设计超过多个职责，应建议拆分。
