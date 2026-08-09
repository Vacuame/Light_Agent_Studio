# 协作规则

本文件是 handoff/report 协作协议的唯一权威来源，定义 Agent 之间如何通过状态层交流文件协作。

文件格式模板见 `rules/context-rules.md`。全局确认原则见 `rules/rules.md`。

## 协作模型

Agent Studio 不替用户判断任务应该如何拆分，也不规定固定的大/中/小任务结构。

任务结构由用户或当前任务 owner 决定。框架只保证：

- 每个顶层任务有独立目录。
- 每个 Agent 窗口有自己的工作区。
- 交接写入接手 Agent 工作区的 `handoff.md`，但必须先有用户明确要求或确认。
- 完成或阶段结论需要向上留痕时，写入当前 Agent 工作区的 `report.md`，但必须先有用户明确要求或确认。
- 顶层任务总览写入 `overview.md`。
- 多个任务或多个 Agent 不会覆盖同一个交流文件。
- 删除任务目录或 Agent 工作区前必须获得用户确认。

任务可以只有一个 Agent 工作区，也可以有多个嵌套或并列工作区。一个 Agent 可以兼任多个角色，但应在工作区目录名或 handoff 中说明职责。

## 目录关系

状态层完整结构见 `rules/context-rules.md`。

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

创建接手 Agent 工作区前，必须先判断接手者与当前 Agent 工作区的关系：

- 如果接手者是在当前工作区拆出的下游执行者、验证者、研究者、实现者或子任务承担者，创建为当前 Agent 工作区的子工作区。
- 如果接手者与当前工作区并列承担同一顶层任务的另一条独立分支，创建为同级工作区。
- 如果接手者只是辅助理解、旁路审查或临时咨询，且不属于当前工作区的下游链路，可以创建为同级旁支，或在用户指定的位置创建。
- 如果无法判断是子级、同级还是旁支，必须列出候选位置并询问用户，不得默认放到顶层任务目录下。

默认原则：从当前 Agent 工作区发出的向下交接，接手工作区应创建为当前 Agent 工作区的子工作区；只有用户明确要求同级、旁支、顶层工作区，或当前工作区不是交接来源时，才创建为顶层任务下的一级工作区。

## 交接与回报方向

`handoff.md` 和 `report.md` 只是上下级或接手关系中的工作交流文件，不是状态机、流程引擎或阶段判定器。

交接和回报只传递接手者或上层继续当前下一步所需的信息。不要把未确认的后续分支、完整角色链路或猜测性任务拆分写成交接要求；如果协作路径依赖未确认选择，先标明 BLOCKED / CONCERNS，并请用户或上层 owner 判断。

```text
handoff.md = 写给下级、下游或接手者，放在接手者 Agent 工作区
report.md  = 写给上级、上层汇总者、任务 owner 或用户，放在当前 Agent 工作区
```

顶层任务目录 `state/tasks/<task-id>/` 不是 Agent 工作区，不直接放 `handoff.md` 或 `report.md`。

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

如果交接给 Developer，还必须写清楚实现落点摘要。

写 `handoff.md` 不代表当前工作区自动结束，不自动要求写当前工作区 `report.md`，也不自动更新 `overview.md`。

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

`report.md` 只表达当前工作区的回报内容，不代表顶层任务自动完成，不自动要求更新 `overview.md`。

### overview 更新

顶层任务 `overview.md` 只记录跨角色、稳定、会影响后续 Agent 的任务级结论。文件职责和格式见 `rules/context-rules.md`。

子级 Agent 写 report 时不自动更新 overview。父级、汇总者或任务 owner 读取 report 后，决定是否建议把其中的稳定结论写入 overview；写入前必须向用户说明拟更新内容并获得确认。

## 任务公共认知

任务级 `docs/*.md` 的职责、格式和维护规则见 `rules/context-rules.md`。

协作层只规定：任务推进中产生、多个 Agent 需要共享、但暂时不适合写入全局 `docs/` 的内容，只有在用户明确要求或确认后，才能写入任务目录下的 `docs/`。

## 状态写入位置

- 顶层任务总览：`state/tasks/<task-id>/overview.md`
- 当前 Agent 回报：`state/tasks/<task-id>/<current-agent-workspace>/report.md`
- 向子 Agent 交接：`state/tasks/<task-id>/<current-agent-workspace>/<child-agent-workspace>/handoff.md`
- 子 Agent 回报：`state/tasks/<task-id>/<current-agent-workspace>/<child-agent-workspace>/report.md`
- 同级或旁支 Agent 交接：`state/tasks/<task-id>/<sibling-or-branch-workspace>/handoff.md`
- 同级或旁支 Agent 回报：`state/tasks/<task-id>/<sibling-or-branch-workspace>/report.md`
- 任务级公共认知：`state/tasks/<task-id>/docs/*.md`，按 `rules/context-rules.md` 和用户确认执行
- 长期事实：全局 `docs/`

## 更新产物层的时机

全局 `docs/` 是正式产物，不要频繁写草稿。

只有在以下情况更新：

- 用户确认方案
- 设计定稿
- 架构决策确认
- 代码实现确认
- 测试结果确认
- 任务准备进入下一阶段

任务过程、交接、回报、阻塞、临时假设写入 `state/`，并按状态层写入确认规则执行。

## 状态层清理

任务关闭需要留痕时，在顶层任务 `overview.md` 或相关 Agent 工作区 `report.md` 中记录结论，写入前必须获得用户确认。

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
> state/tasks/<task-id>/docs/*.md
> 父级 Agent 工作区 report.md
> 当前 Agent 工作区 handoff.md
> 当前 Agent 工作区 report.md
> Adviser 的 derived context
```

如果冲突影响实现，必须先问用户，不得自行选择。

如果模块设计中的实现落点与真实代码冲突，Developer 必须反馈给 Module Designer 或用户确认，不得自行改变模块边界或代码层级。

如果两个任务需要修改同一文件或同一职责边界，必须在相关工作区的 `report.md` 中标明冲突，并由用户或共同上层 owner 决定如何处理。

## 角色责任边界

角色职责和权限边界见 `agents/<role>.md`。本文件只定义协作方向，不授予角色额外权限。

角色可以提出跨领域建议，但不能直接越权修改其他角色负责的权威产物。

## 协作中的读文件原则

不要让每个角色读所有文件。

读取范围由以下部分组合：

```text
rules.md 通用基线 + context-rules 状态读取规则 + 当前角色 + 当前技能 + 相关产物 + 对应质量门
```

如果某个文件只是背景知识，先判断是否必要。避免把无关上下文塞给 Agent。

## 交接前检查

交接前必须确认：

- 当前产物是否达到对应质量门要求
- 风险是否写清楚
- 临时假设是否标明
- 下一个角色需要读哪些文件
- 接手工作区与当前工作区的关系是否已判断清楚：子级、同级或旁支
- 要写入哪个 Agent 工作区的 `handoff.md`
- 拟写入的 `handoff.md` 完整路径是否已向用户说明
- 是否已有用户明确要求或确认写入该 `handoff.md`

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
- 创建或修改任务级 `docs/*.md`
- 修改顶层任务 `overview.md`
- 修改规则、角色、技能或质量门
- 删除或移动文件
- 删除任务目录或 Agent 工作区
- 引入依赖
- 接受 CONCERNS 风险继续推进
- 关闭任务

创建或修改 `handoff.md` / `report.md` 前，必须说明拟写入的完整路径。

用户确认必须是明确文字，例如：

```text
可以
同意
按这个写
写入
接受风险继续
```

用户让 Agent “继续分析”“给建议”“先看看”不等于授权写文件。
