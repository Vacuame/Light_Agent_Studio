# 上下文规则

上下文规则用于防止会话断片、压缩后遗忘、交接混乱。

## 核心原则

文件是长期记忆，对话只是临时过程。

重要信息不要只留在聊天里。只要会影响后续工作，就要写入 `state/` 或 `docs/`。

`state/` 是当前怎么接着干；`docs/` 是已确认的项目事实。

## 状态层组织

状态层采用轻量树形任务工作区：

```text
state/tasks/<task-id>/
  overview.md
  <agent-workspace>/
    handoff.md
    report.md
    <child-agent-workspace>/
      handoff.md
      report.md
```

说明：

- `state/tasks/<task-id>/` 是用户明确开启的顶层任务目录。
- `overview.md` 是顶层任务总览，记录任务背景、目标、当前进展、重要文件、疑点、共识和会影响后续 Agent 的稳定结论。
- `<agent-workspace>/` 是某个 Agent 窗口的工作区，每个 Agent 窗口都必须定位或创建自己的工作区。
- `handoff.md` 是父级或上游写给当前工作区的交接。
- `report.md` 是当前工作区写给父级、上层汇总者或用户的回报。
- 嵌套工作区表示父子关系；同级工作区表示并列或旁支关系。
- 目录树就是定位线索，不额外维护任务索引或状态面板。

## 顶层任务 overview.md

`overview.md` 推荐包含：

```markdown
# 任务总览

## 任务目标

## 背景

## 当前进展

## 重要文件

## 已确认共识

## 疑点与阻塞

## 重要关系说明

## 最终结论
```

`overview.md` 只写跨角色、稳定、会影响后续工作的内容。不要复制完整 `handoff.md` 或 `report.md`，不要写成聊天流水账。

子级 Agent 写 `report.md` 时不自动更新 `overview.md`。父级、汇总者或任务 owner 读取 report 后，再决定哪些稳定结论进入 `overview.md`。

## Agent 工作区

每个 Agent 窗口必须有自己的工作区。

工作区目录名应表达角色组合和职责，例如：

```text
01-architecture-module-login/
02-developer-login-api/
03-adviser-context/
```

角色可以组合，目录名不依赖固定角色枚举。

如果当前顶层任务目录或 Agent 工作区不明确，先根据：

- 用户当前任务描述
- 顶层任务目录名
- 顶层任务 `overview.md`
- 工作区目录名
- 当前工作区或父级工作区的 `handoff.md` / `report.md`

自行定位。仍无法唯一定位时，列出候选并询问用户。

## 压缩前

如果会话将被压缩或任务很长，当前 Agent 应先更新自己的工作区状态：

1. 更新当前工作区 `report.md`，写清楚已完成、未完成、风险和下一步。
2. 如果需要交给下游 Agent，在子工作区写 `handoff.md`。
3. 如果当前 Agent 是父级、汇总者或任务 owner，并且已经读取子级 report，必要时更新顶层任务 `overview.md`。

并写清楚：

- 已经做完什么
- 还没做什么
- 哪些文件是权威来源
- 下个角色或上层 owner 应该从哪里继续
- 当前顶层任务目录和 Agent 工作区路径

## 压缩后

压缩或换窗口后，第一步必须读取：

1. 当前顶层任务的 `overview.md`
2. 当前 Agent 工作区的 `handoff.md`（如果存在）
3. 当前 Agent 工作区的 `report.md`（如果存在）
4. 必要的父级、子级或兄弟工作区 `report.md`
5. 当前任务相关的正式产物文件

不要根据压缩摘要直接继续做复杂决策。

## handoff 与 report

### handoff.md 推荐格式

`handoff.md` 是向下交接文件。只有需要交给另一个角色、Agent 或子工作区时才需要。

```markdown
# 任务交接

## 交接来源

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

`report.md` 是向上回报文件。当前工作区完成、阶段结束、阻塞、放弃或需要上层判断时填写。

```markdown
# 任务完成报告

## 回报给谁

## 本工作区结论

PASS / CONCERNS / BLOCKED / DROPPED

## 完成内容

## 修改或产出文件

## 验证结果

## 未完成项

## 风险与注意事项

## 对上层任务的影响

## 建议写入 overview.md

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

## 长任务更新频率

长任务不需要每一步都更新正式产物，但要定期更新状态。

建议：

- 每完成一个小阶段，更新当前 Agent 工作区的 `report.md`
- 每次向下交接，更新接手 Agent 工作区的 `handoff.md`
- 每次向上回报，更新当前 Agent 工作区的 `report.md`
- 每次用户确认会影响后续 Agent 的任务级结论，父级或汇总者更新顶层任务 `overview.md`
- 每次用户确认长期结论，再更新 `docs/`

## 状态层与产物层

```text
state/ = 当前怎么接着干
docs/  = 已确认的项目事实
```

如果只是临时进度、阻塞、下一步、交接或回报，写入 `state/`。

如果是长期会被后续角色依赖的事实，写入 `docs/`。
