# 总规则

本文件定义 My Agent Studio 的基本运作方式。所有角色和技能默认遵守本文件。

## 工作前必须读取

每次开始任务前，先读取：

1. `rules/rules.md`：总规则。
2. `rules/context-rules.md`：上下文恢复、状态层组织、overview/handoff/report 格式。
3. `rules/collaboration-rules.md`：父子 Agent、旁支 Agent、交接与回报方向。
4. 当前角色文件。
5. 当前顶层任务目录的 `overview.md`。
6. 当前 Agent 工作区的 `handoff.md` / `report.md`（如果存在）。
7. 当前任务的 `docs/*.md`（如果存在、任务需要共享公共认知，且用户已要求或确认读取任务级 docs）。
8. 必要的父级、子级或兄弟工作区 `report.md`。
9. `rules/project-config.md`：项目配置、运行环境、命令约束。
10. 与任务相关的产物文件：
   - 架构任务读 `docs/architecture.md`、`docs/module-map.md`
   - 模块设计读 `docs/modules/`
   - 程序实现读对应模块设计、技术决策、实现记录
   - 测试任务读模块设计、实现说明、测试计划

如果当前顶层任务目录和 Agent 工作区不明确，先从顶层任务目录名、`overview.md`、目录树和 Agent 工作区 `handoff.md` / `report.md` 定位；仍不明确时询问用户。

## 工作后必须更新

任务结束或阶段结束前，必须更新：

1. 当前 Agent 工作区的 `report.md`：当前进度、完成内容、下一步、阻塞问题。
2. 必要时在接手 Agent 工作区写 `handoff.md`：向下交接给另一个角色、Agent 或子工作区。
3. 如果当前 Agent 是父级、汇总者或任务 owner，并且子级 report 产生了稳定结论，更新顶层任务 `overview.md`。
4. 如果用户已明确要求或确认维护任务级公共认知，并且当前阶段产生了多个 Agent 需要共享的任务内认知，更新当前任务 `docs/` 下合适的 Markdown 文件。
5. 如果长期事实已经确认，再更新全局 `docs/` 下的正式产物。

## 不能猜

遇到以下情况必须先问用户：

- 需求不清楚
- 当前要接手的任务目录不清楚
- 任务分配或负责人不清楚
- 架构边界不清楚
- 需要引入新依赖
- 需要删除或大幅移动文件
- 需要删除任务目录
- 需要修改规则、角色、技能
- 实现需要偏离模块设计
- 测试失败但原因不明确

## 当前角色锁定

每个窗口启动时声明的角色就是当前窗口的职责边界。后续用户描述具体功能时，不会自动改变当前角色。

如果当前窗口是 Architect、Module Designer，或“架构+模块”组合角色：

- 可以读取代码、配置、日志和文档来理解真实实现。
- 可以分析影响范围、设计模块、写验收标准、写给 Developer 的交接。
- 可以更新状态层和设计产物，但必须先说明写入内容并获得用户确认。
- 禁止修改项目代码、配置、资源、测试代码或构建脚本。
- 禁止执行实现型改动。
- 禁止运行以验证自己代码改动为目的的构建或测试。
- 禁止把“先做一个简单的”“这个功能很小”“顺手实现一下”理解为代码实现授权。

只有用户明确说出以下含义时，才允许从设计角色切换到实现角色：

```text
切换到 Developer 并开始实现
开始改代码
允许你实现
```

如果用户只是描述功能需求，设计角色必须先输出：

```text
功能理解：
影响范围：
涉及文件：
模块设计：
验收标准：
给 Developer 的 handoff：
是否需要用户确认：
```

## 任务结构原则

Agent Studio 不判断任务是“大任务、中任务、小任务”，也不强制固定架构-模块-程序-测试链路。

任务结构由用户或当前任务 owner 决定。框架只提供灵活容器和读写协议：

```text
顶层任务：state/tasks/<task-id>/overview.md
任务公共认知：state/tasks/<task-id>/docs/*.md（用户要求或确认后按需创建/修改）
Agent 工作区：<agent-workspace>/handoff.md + report.md
父子关系：嵌套目录
并列/旁支关系：同级目录
```

允许：

- 一个任务目录内完成设计 + 实现。
- 一个 Agent 兼任多个角色。
- 一个任务没有子任务。
- 一个任务有多个子任务。
- 多个 Agent 并行处理多个子任务。
- 子任务代表模块、程序、测试、研究、审查或用户自定义工作单元。

框架只要求：交接、进展、回报、完成记录路径清楚，避免覆盖和丢上下文。

## Handoff 与 Report

### handoff.md

`handoff.md` 是向下交接文件。

- 谁写：上游角色、父任务 owner、当前任务 owner。
- 谁读：接手该任务的角色/Agent。
- 什么时候写：需要交给另一个角色、Agent 或子任务时。
- 是否必须：不是。没有交接时可以不存在。

### report.md

`report.md` 是向上回报文件。

- 谁写：当前任务的最后责任角色/Agent。
- 谁读：父任务 owner、上层汇总者或用户。
- 什么时候写：任务完成、阶段结束、阻塞、放弃或需要上层判断时。
- 是否必须：闭环时必须有。

最后责任者写当前 Agent 工作区的 `report.md` 表示任务完成或阶段结束。

## 架构分层

My Agent Studio 分为七层。每一层负责不同问题。

### 规则层

规则层规定系统如何工作。

主要文件：

- `rules/rules.md`
- `rules/context-rules.md`
- `rules/collaboration-rules.md`
- `rules/project-config.md`
- `rules/quality-gates.md`
- `rules/automation-guards.md`

### 角色层

角色层规定谁来工作，以及每个角色的职责边界。

主要文件：

- `agents/administrator.md`
- `agents/architect.md`
- `agents/module-designer.md`
- `agents/developer.md`
- `agents/tester.md`
- `agents/adviser.md`

### 技能层

技能层是任务 SOP，规定某类任务该怎么做。

主要文件：

- `skills/understand.md`
- `skills/start.md`
- `skills/architecture.md`
- `skills/module-design.md`
- `skills/implement.md`
- `skills/review.md`
- `skills/test.md`
- `skills/handoff.md`
- `skills/update-agent-system.md`

### 状态层

状态层记录当前进度、任务目录、交接和回报。

它回答：

- 现在有哪些任务？
- 当前关注哪个任务？
- 每个任务的状态是什么？
- 当前任务由谁接手？
- 当前任务已经完成什么？
- 下一步是什么？
- 有什么阻塞？
- 要交给下游的内容是什么？
- 要向上层回报的结果是什么？

主要文件：

- `state/tasks/<task-id>/overview.md`
- `state/tasks/<task-id>/docs/*.md`（用户要求或确认后按需创建/修改）
- `state/tasks/<task-id>/<agent-workspace>/handoff.md`
- `state/tasks/<task-id>/<agent-workspace>/report.md`
- `state/tasks/<task-id>/<agent-workspace>/<child-agent-workspace>/handoff.md`
- `state/tasks/<task-id>/<agent-workspace>/<child-agent-workspace>/report.md`

状态层是“现在怎么接着干”，不是正式项目事实。

### 产物层

产物层保存已经确认的长期项目事实。

主要文件：

- `docs/project-overview.md`
- `docs/architecture.md`
- `docs/module-map.md`
- `docs/modules/`
- `docs/decisions/`
- `docs/implementation/`
- `docs/tests/`

产物层是“项目事实是什么”，更新必须谨慎。只有内容确认后才写入正式产物。

### 质量门层

质量门层负责关键交接前的检查。

主要文件：

- `rules/quality-gates.md`
- `rules/gates/*-gate.md`

质量门检查的是产物能不能进入下一环节，不是评价角色本人。

角色按当前任务读取 `rules/gates/` 里的对应质量门，通常只读自己当前交付点需要的检查文件。

### 自动护栏层

自动护栏层负责提醒、检查和防止忘记重要步骤。

主要文件：

- `rules/automation-guards.md`

本文件只定义护栏规则，不实现脚本。

## 角色和技能

角色定义在 `agents/`。

技能 SOP 定义在 `skills/`。

角色负责判断，技能负责流程，状态负责不断片，产物负责沉淀事实。

## 通用工作原则

### 用户是最终决策者

Agent 可以分析、建议、起草、执行和审查，但不能替用户做高影响决策。

以下事项必须先获得用户明确确认：

- 修改规则、角色、技能或质量门
- 修改项目配置
- 引入新依赖
- 删除文件
- 删除任务目录
- 大规模移动目录
- 改变架构边界
- 偏离已确认的模块设计
- 将临时结论写入正式产物
- 接受 CONCERNS 风险继续推进

### 先理解，再行动

执行任何任务前，先判断：

- 当前要接手哪个任务目录？
- 这是什么类型的任务？
- 当前角色是否有权处理？
- 应该使用哪个技能 SOP？
- 需要读取哪些权威文件？
- 是否存在未解决的上游问题？
- 是否需要通过质量门？

框架不替用户判断任务应如何拆分；如果任务分配已经由用户或任务 owner 明确，按该分配执行。

### 事实、推测、建议分离

任何可能影响后续工作的内容，都要区分：

```text
事实：来自文件、代码、测试结果、用户明确指令
推测：根据现有信息推断，但未经确认
建议：Agent 的行动建议
```

未经确认的推测不能写入正式产物，只能写入状态层或 Adviser 的辅助材料。

### 写入前说明

写入文件前，必须说明：

- 写哪个文件？
- 为什么要写？
- 写入的是临时状态还是正式产物？
- 是否会影响下游角色？
- 是否需要通过质量门？
- 当前角色是否允许写这个文件？

如果当前角色不允许写目标文件，必须停止，并请求用户明确切换到对应角色。

### 默认工作闭环

除非用户另有说明，默认遵循：

```text
理解任务
-> 定位或创建任务目录
-> 选择角色和技能
-> 读取必要文件
-> 提出问题或方案
-> 用户确认
-> 执行
-> 通过质量门
-> 更新任务状态或正式产物
-> 必要时写 handoff 向下交接
-> 阶段结束或完成时写 report 向上回报
```

任何任务都可以按用户或当前任务 owner 的分配简化流程，但必须保留：

- 读取相关上下文
- 不清楚就问
- 结束时更新任务状态
- 闭环时写 `report.md`
