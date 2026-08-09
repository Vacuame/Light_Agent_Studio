# 协作规则

本文件定义角色之间如何通过文件协作。

## 协作模型

Agent Studio 不替用户判断任务应该如何拆分，也不规定固定的大/中/小任务结构。

任务结构由用户或当前任务 owner 决定。框架只保证：

- 每个顶层任务有独立目录。
- 每个 Agent 窗口有自己的工作区。
- 交接写入接手 Agent 工作区的 `handoff.md`，但必须先有用户明确要求或确认。
- 完成或阶段结论需要向上留痕时，写入当前 Agent 工作区的 `report.md`，但必须先有用户明确要求或确认。
- 顶层任务总览写入 `overview.md`。
- 多个任务或多个 Agent 不会覆盖同一个交接文件。
- 删除任务目录或 Agent 工作区前必须获得用户确认。

任务可以只有一个 Agent 工作区，也可以有多个嵌套或并列工作区。一个 Agent 可以兼任多个角色，但应在工作区目录名或 handoff 中说明职责。

## 目录关系

状态层目录结构：

```text
state/tasks/<task-id>/
  overview.md
  docs/
    <task-public-doc>.md
  <agent-workspace>/
    handoff.md
    report.md
    <child-agent-workspace>/
      handoff.md
      report.md
```

判断关系：

- `state/tasks/<task-id>/` 是顶层任务，不是 Agent 工作区。
- 直接位于顶层任务目录下的文件夹，是该任务的一级 Agent 工作区。
- 位于某个 Agent 工作区里面的文件夹，是该工作区的子 Agent 工作区。
- 同一层级的工作区是兄弟、并列或旁支关系。
- Adviser、Reviewer、Researcher 等辅助角色可以作为同级旁支，也可以挂在某个局部分支下。

示例：

```text
state/tasks/login-refactor/
  overview.md
  01-architecture-module-login/
    handoff.md
    report.md
    01-developer-login-api/
      handoff.md
      report.md
  02-adviser-context/
    handoff.md
    report.md
```

这里：

- `01-architecture-module-login/` 是一级 Agent 工作区。
- `01-developer-login-api/` 是 `01-architecture-module-login/` 的子 Agent 工作区。
- `02-adviser-context/` 与 `01-architecture-module-login/` 同级，是旁支工作区。

## 交接与回报方向

`handoff.md` 和 `report.md` 只是上下级或接手关系中的工作交流文件，不是状态机、流程引擎或阶段判定器。

交接和回报只传递接手者或上层继续当前下一步所需的信息。不要把未确认的后续分支、完整角色链路或猜测性任务拆分写成交接要求；如果协作路径依赖未确认选择，先标明 BLOCKED / CONCERNS，并请用户或上层 owner 判断。

```text
handoff.md = 写给下级、下游或接手者，放在接手者 Agent 工作区
report.md  = 写给上级、上层汇总者、任务 owner 或用户，放在当前 Agent 工作区
overview.md = 顶层任务总览
```

### 向下交接

当一个任务要交给另一个角色、Agent 或子工作区时，父级或上游先确认接手对象和拟写摘要，并询问用户是否写入；用户确认后，在接手 Agent 工作区写入 `handoff.md`。

交接必须写清楚：

- 交接来源
- 交接给谁
- 接手什么
- 需要读取哪些文件
- 哪些内容已经确定
- 哪些内容只是临时假设
- 风险
- 下一步建议

如果交接给 Developer，还必须写清楚：

- 涉及文件/目录
- 归属类、组件、模块或服务
- 建议新增或修改的方法、事件、接口或配置点
- 调用入口和数据流出口
- 不应放置的位置
- 需要 Developer 验证的不确定点

### 向上回报

当一个 Agent 需要向父级、上层汇总者、任务 owner 或用户说明当前结果、阻塞、风险或请求判断时，先在对话中说明结果/阻塞/风险/请求判断；用户确认需要留痕后，写入当前 Agent 工作区的 `report.md`。

回报必须写清楚：

- 回报给谁
- 本工作区结论：PASS / CONCERNS / BLOCKED / DROPPED
- 完成内容
- 修改或产出文件
- 验证结果
- 未完成项
- 风险与注意事项
- 对上层任务的影响
- 建议下一步

父级 Agent、任务 owner 或上层汇总者读取子工作区的 `report.md`，决定继续、返工、关闭、记录完成或再拆工作区。

### overview 更新

顶层任务 `overview.md` 只记录跨角色、稳定、会影响后续 Agent 的任务级结论。

子级 Agent 写 report 时不自动更新 overview。父级、汇总者或任务 owner 读取 report 后，决定是否把其中的稳定结论写入 overview。

## 任务公共认知

任务推进中产生、多个 Agent 需要共享、但暂时不适合写入全局 `docs/` 的内容，在用户明确要求或确认后，写入任务目录下的 `docs/`：

```text
state/tasks/<task-id>/docs/<task-public-doc>.md
```

使用规则：

- 只有在用户明确要求维护任务级公共认知，或用户确认当前任务需要任务级 docs 后，Agent 才能创建或写入任务目录 `docs/` 下的 Markdown 文件。
- 用户已授权任务级 docs 后，Agent 可以把和自己工作有关的公共发现、假设、疑点、候选决策和参考线索追加到合适的 Markdown 文件中；如果没有合适文件，先按内容命名创建新的 Markdown 文件。
- 写入时必须标明来源、确定性、影响范围和待确认问题。
- 单个 Agent 的完整过程仍写自己的 `report.md`，不要复制到任务级 `docs/`。
- 父级、汇总者或任务 owner 负责定期整理公共认知，必要时把稳定结论提炼到 `overview.md`。
- 经用户或权威角色确认、具有长期价值的内容，再写入全局 `docs/`。

## 状态写入位置

顶层任务总览写入：

```text
state/tasks/<task-id>/overview.md
```

Agent 交接和回报写入：

```text
state/tasks/<task-id>/<agent-workspace>/handoff.md
state/tasks/<task-id>/<agent-workspace>/report.md
```

子 Agent 交接和回报写入：

```text
state/tasks/<task-id>/<agent-workspace>/<child-agent-workspace>/handoff.md
state/tasks/<task-id>/<agent-workspace>/<child-agent-workspace>/report.md
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

任务过程、交接、回报、阻塞、临时假设写入 `state/`。

## 状态层清理

任务关闭需要留痕时，在顶层任务 `overview.md` 或相关 Agent 工作区 `report.md` 中记录结论。

任务关闭后的处理方式：

1. 保留在 `state/tasks/<task-id>/`，在 `overview.md` 标记结论。
2. 在用户明确确认后删除任务目录。

删除前必须确认任务没有需要保留的长期价值。删除顶层任务目录或 Agent 工作区是破坏性操作。

## 冲突处理

当文件之间冲突时，优先级如下：

```text
用户最新明确指令
> docs/decisions/
> docs/architecture.md
> docs/modules/
> state/tasks/<task-id>/overview.md
> 父级 Agent 工作区 report.md
> 当前 Agent 工作区 handoff.md
> 当前 Agent 工作区 report.md
> Adviser 的 derived context
```

如果冲突影响实现，必须先问用户，不得自行选择。

如果模块设计中的实现落点与真实代码冲突，Developer 必须反馈给 Module Designer 或用户确认，不得自行改变模块边界或代码层级。

如果两个任务需要修改同一文件或同一职责边界，必须在相关工作区的 `report.md` 中标明冲突，并由用户或共同上层 owner 决定如何处理。

## 角色责任边界

```text
Administrator：维护 Agent 系统本身
Architect：维护整体架构和模块边界
Module Designer：把模块设计到可实现、可测试
Developer：按模块设计实现代码
Tester：按验收标准测试和判断能否关闭
Adviser：解释、问答、辅助理解，不产出权威设计
```

角色可以提出跨领域建议，但不能直接越权修改其他角色负责的权威产物。

## 协作中的读文件原则

不要让每个角色读所有文件。

读取范围应遵循：

```text
总规则 + 当前顶层任务 overview + 当前 Agent 工作区 + 当前角色 + 当前技能 + 相关产物 + 对应质量门
```

如果某个文件只是背景知识，先判断是否必要。避免把无关上下文塞给 Agent。

## 交接前检查

交接前必须确认：

- 当前产物是否达到对应质量门要求
- 风险是否写清楚
- 临时假设是否标明
- 下一个角色需要读哪些文件
- 要写入哪个 Agent 工作区的 `handoff.md`
- 是否已有用户明确要求或确认写入该 `handoff.md`
- 是否需要用户确认

## 回报前检查

回报前必须确认：

- 本工作区结论是否清楚
- 完成内容是否写清楚
- 修改或产出文件是否列出
- 验证结果是否写清楚
- 未完成项和风险是否写清楚
- 上层任务或用户下一步是否清楚
- 要写入哪个 Agent 工作区的 `report.md`
- 是否已有用户明确要求或确认写入该 `report.md`

## 用户确认机制

以下动作前必须请用户确认：

- 写入正式产物
- 创建或修改 Agent 工作区的 `handoff.md` / `report.md`
- 修改规则、角色、技能
- 删除或移动文件
- 删除任务目录或 Agent 工作区
- 引入依赖
- 接受 CONCERNS 风险继续推进
- 关闭任务

用户确认可以是明确文字，例如：

```text
可以
同意
按这个写
接受风险继续
```
