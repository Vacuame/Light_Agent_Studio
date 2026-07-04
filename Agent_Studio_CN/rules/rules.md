# 总规则

本文件定义 My Agent Studio 的基本运作方式。所有角色和技能默认遵守本文件。

## 工作前必须读取

每次开始任务前，先读取：

1. `state/active.md`：当前任务、进度、下一步、阻塞问题。
2. `rules/project-config.md`：项目配置、运行环境、命令约束。
3. 与任务相关的产物文件：
   - 架构任务读 `docs/architecture.md`、`docs/module-map.md`
   - 模块设计读 `docs/modules/`
   - 程序实现读对应模块设计、技术决策、实现记录
   - 测试任务读模块设计、实现说明、测试计划

## 工作后必须更新

任务结束前，必须更新：

1. `state/active.md`：当前进度、完成内容、下一步。
2. 必要时更新 `state/handoff.md`：给下一个角色的临时交接说明。
3. 如果长期事实已经确认，再更新 `docs/` 下的正式产物。

## 不能猜

遇到以下情况必须先问用户：

- 需求不清楚
- 架构边界不清楚
- 需要引入新依赖
- 需要删除或大幅移动文件
- 需要修改规则、角色、技能
- 实现需要偏离模块设计
- 测试失败但原因不明确

## 架构分层

My Agent Studio 分为七层。每一层负责不同问题。

### 规则层

规则层规定系统如何工作。

它回答：

- 开始任务前要读什么？
- 结束任务前要更新什么？
- 不清楚时怎么处理？
- 哪些操作必须先问用户？
- 项目环境和技术约束是什么？

主要文件：

- `rules/rules.md`
- `rules/context-rules.md`
- `rules/collaboration-rules.md`
- `rules/project-config.md`
- `rules/quality-gates.md`
- `rules/automation-guards.md`

### 角色层

角色层规定谁来工作，以及每个角色的职责边界。

它回答：

- Architect 负责什么？
- Module Designer 负责什么？
- Developer 能不能改架构？
- Tester 能不能改代码？
- Adviser 写的内容是不是权威来源？
- Administrator 什么时候可以修改 Agent 架构？

主要文件：

- `agents/administrator.md`
- `agents/architect.md`
- `agents/module-designer.md`
- `agents/developer.md`
- `agents/tester.md`
- `agents/adviser.md`

### 技能层

技能层是任务 SOP，规定某类任务该怎么做。

它回答：

- 做架构设计时按什么步骤？
- 做模块设计时要读哪些文件？
- 实现代码前要确认什么？
- 测试前要看哪些验收标准？
- 交接时要写什么？

主要文件：

- `skills/understand.md`
- `skills/architecture.md`
- `skills/module-design.md`
- `skills/implement.md`
- `skills/review.md`
- `skills/test.md`
- `skills/handoff.md`
- `skills/update-agent-system.md`

### 状态层

状态层记录当前进度和临时交接。

它回答：

- 现在正在做什么？
- 当前由哪个角色接手？
- 已经完成了什么？
- 下一步是什么？
- 有什么阻塞？
- 要交给下一个角色的临时说明是什么？

主要文件：

- `state/active.md`
- `state/handoff.md`
- `state/session-log.md`

状态层是“现在怎么接着干”，不是正式项目事实。

### 产物层

产物层保存已经确认的长期项目事实。

它回答：

- 项目总体目标是什么？
- 总体架构是什么？
- 有哪些模块？
- 每个模块如何设计？
- 做过哪些重要技术决策？
- 实现后有哪些变更？
- 测试计划和测试结果是什么？

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

它回答：

- 架构能不能交给模块设计？
- 模块设计能不能交给开发？
- 代码能不能交给测试？
- 测试结果能不能支持关闭任务？
- 修改规则会不会造成副作用？

主要文件：

- `rules/quality-gates.md`

质量门检查的是产物能不能进入下一环节，不是评价角色本人。

### 自动护栏层

自动护栏层负责提醒、检查和防止忘记重要步骤。

它回答：

- 会话开始时要提醒读什么？
- 压缩前是否保存状态？
- 危险操作前是否确认？
- 阶段完成前是否得到用户确认？

主要文件：

- `rules/automation-guards.md`

当前版本只定义护栏规则，不实现脚本。

## 角色和技能

角色定义在 `agents/`。

技能 SOP 定义在 `skills/`。

角色负责判断，技能负责流程，状态负责不断片，产物负责沉淀事实。
