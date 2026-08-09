# 上下文规则

上下文规则用于防止会话断片、压缩后遗忘、交接混乱。

## 核心原则

文件是长期记忆，对话只是临时过程。

重要信息不要只留在聊天里。只要会影响后续工作，就要写入 `state/` 或 `docs/`。

`state/` 是当前怎么接着干；`docs/` 是已确认的项目事实。

## 全局状态与任务状态

`state/tasks/<task-id>/overview.md` 是顶层任务总览，至少记录：

- 当前顶层任务
- 活跃任务列表
- 阻塞任务列表
- 最近交接/回报摘要
- `state/tasks/README.md` 入口

`state/tasks/README.md` 是任务目录说明，至少记录：

- 任务 ID
- 标题
- 父任务
- 状态
- 当前角色/负责人
- 路径
- 最近更新

每个任务目录至少包含：

```text
overview.md
report.md
report.md
```

按需包含：

```text
handoff.md
相关工作区 report
嵌套 Agent 工作区
```

框架不判断任务大小，也不强制任务层级。任务目录、子任务和角色分配由用户或当前任务 owner 决定。

## 压缩前

如果会话将被压缩或任务很长，先更新：

1. `state/tasks/<task-id>/overview.md`
2. `state/tasks/README.md`
3. 当前 Agent 工作区的 `report.md`
4. 必要时更新当前 Agent 工作区的 `handoff.md` 或 `report.md`

并写清楚：

- 已经做完什么
- 还没做什么
- 哪些文件是权威来源
- 下个角色或上层 owner 应该从哪里继续
- 当前顶层任务目录和 Agent 工作区路径

## 压缩后

压缩或换窗口后，第一步必须读取：

1. `state/tasks/<task-id>/overview.md`
2. `state/tasks/README.md`
3. 当前顶层任务的 `overview.md`
4. 当前 Agent 工作区的 `report.md`
5. 当前 Agent 工作区的 `handoff.md` 或 `report.md`（如果存在）
6. 当前任务相关的正式产物文件

不要根据压缩摘要直接继续做复杂决策。

如果当前顶层任务目录和 Agent 工作区不明确，先从 `state/tasks/<task-id>/overview.md` 和 `state/tasks/README.md` 定位；仍不明确时询问用户。

## handoff 与 report

### handoff.md 推荐格式

`handoff.md` 是向下交接文件。只有需要交给另一个角色、Agent 或子任务时才需要。

```markdown
# 任务交接

## 交接给谁

## 接手什么

## 必读文件

## 已确认内容

## 临时假设

## 风险

## 实现落点摘要

## 下一步
```

### report.md 推荐格式

`report.md` 是向上回报文件。任务完成、阶段结束、阻塞、放弃或需要上层判断时填写。

```markdown
# 任务完成报告

## 回报给谁

## 本任务结论

PASS / CONCERNS / BLOCKED / DROPPED

## 完成内容

## 修改或产出文件

## 验证结果

## 未完成项

## 风险与注意事项

## 对上层任务的影响

## 建议下一步
```

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

## active.md 推荐格式

```markdown
# 当前任务面板

## 当前顶层任务

## 活跃任务

## 阻塞任务

## 最近交接/回报摘要

## 任务目录说明

## 下一步
```

## 任务目录推荐格式

```text
state/tasks/<task-id>/
  overview.md
  report.md
  report.md
  handoff.md   # 按需
  相关工作区 report     # 按需
  嵌套 Agent 工作区    # 按需
```

`overview.md` 推荐包含：

```markdown
# 任务元信息

## 任务 ID

## 标题

## 父任务

## 子任务

## 状态

created / active / handoff / reported / done / blocked / dropped / 完成记录d

## 当前角色/负责人

## 关联正式产物

## 关闭或完成记录策略
```

`report.md` 推荐包含：

```markdown
# 任务进展

## 当前进展

## 已完成

## 未完成

## 阻塞问题

## 下一步
```

## session-log.md 使用规则

`state/session-log.md` 用于记录重要历史摘要，不要写成聊天流水账。

适合记录：

- 完成一个阶段
- 做出一个关键决策
- 修改规则、角色、技能
- 发生一次重要返工
- 发现一个长期风险
- 任务完成记录或删除摘要

完整任务正文保存在对应任务目录，不写入 `session-log.md`。

## 长任务更新频率

长任务不需要每一步都更新正式产物，但要定期更新状态。

建议：

- 每完成一个小阶段，更新当前 Agent 工作区的 `report.md`
- 每次向下交接，更新对应任务目录下的 `handoff.md`
- 每次向上回报，更新对应任务目录下的 `report.md`
- 每次任务状态变化，更新 `state/tasks/README.md` 和 `state/tasks/<task-id>/overview.md`
- 每次用户确认长期结论，再更新 `docs/`

## 状态层与产物层

```text
state/ = 当前怎么接着干
docs/  = 已确认的项目事实
```

如果只是临时进度、阻塞、下一步、交接或回报，写入 `state/`。

如果是长期会被后续角色依赖的事实，写入 `docs/`。
