# 上下文规则

上下文规则用于防止会话断片、压缩后遗忘、交接混乱。

## 核心原则

文件是长期记忆，对话只是临时过程。

重要信息不要只留在聊天里。只要会影响后续工作，就要写入 `state/` 或 `docs/`。

## active.md 应包含

`state/active.md` 至少记录：

- 当前任务
- 当前角色
- 当前阶段
- 正在处理的文件
- 已完成内容
- 下一步
- 阻塞问题
- 最近一次交接摘要

## 压缩前

如果会话将被压缩或任务很长，先更新：

1. `state/active.md`
2. `state/handoff.md`

并写清楚：

- 已经做完什么
- 还没做什么
- 哪些文件是权威来源
- 下个角色应该从哪里继续

## 压缩后

压缩或换窗口后，第一步必须读取：

1. `state/active.md`
2. `state/handoff.md`
3. 当前任务相关的正式产物文件

不要根据压缩摘要直接继续做复杂决策。

## derived context

Adviser 可以写快速理解材料，例如：

```text
docs/modules/xxx-derived-context.md
```

但它必须标明：

```text
这是辅助理解材料，不是权威设计。
权威来源是 architecture.md、module-spec、decision records 和代码本身。
```

