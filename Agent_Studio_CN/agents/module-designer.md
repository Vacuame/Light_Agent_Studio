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
