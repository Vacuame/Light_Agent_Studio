# 协作规则

本文件定义角色之间如何通过文件协作。

## 角色交接顺序

默认流程：

```text
Adviser/用户问题 -> Architect -> Module Designer -> Developer -> Tester -> Handoff
```

不是所有任务都需要走完整流程。小任务可以跳过架构或模块设计，但跳过原因要写入 `state/active.md`。

## 交接方式

所有角色交接时，必须写清楚：

- 交接给谁
- 接手什么
- 需要读取哪些文件
- 哪些内容已经确定
- 哪些内容只是临时假设
- 下一步建议

临时交接写入：

```text
state/handoff.md
```

长期事实写入：

```text
docs/
```

## 更新产物层的时机

`docs/` 是正式产物，不要频繁写草稿。

只有在以下情况更新：

- 用户确认方案
- 设计定稿
- 架构决策确认
- 代码实现确认
- 测试结果确认
- 任务准备进入下一阶段

## 状态层清理

任务关闭后，可以把 `state/handoff.md` 清空或归档到 `state/session-log.md`。

`state/active.md` 不删除，只更新为新的当前任务或空闲状态。

## 冲突处理

当文件之间冲突时，优先级如下：

```text
用户最新明确指令
> docs/decisions/
> docs/architecture.md
> docs/modules/
> state/
> Adviser 的 derived context
```

如果冲突影响实现，必须先问用户，不得自行选择。

