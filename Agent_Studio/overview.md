# Agent Studio 内部导览

这是一个轻量级、通用型 Agent 工作流框架。

它的目标不是模拟一个大型组织，而是把常见 AI 协作流程拆成少数稳定角色，让 Agent 在多轮任务中不丢上下文、不乱改边界、不把临时判断当成长期事实。

## 核心分层

```text
规则层：规定怎么工作
角色层：规定谁来工作
技能层：规定某类任务怎么做
状态层：用树形任务目录记录 overview、Agent 工作区、交接和回报
产物层：保存已经确认的项目事实
质量门层：检查关键产物能否交接、回报或关闭
自动护栏层：提醒、检查、防止忘记重要步骤
```

## 默认角色

```text
Administrator    维护 Agent 架构本身
Architect        负责总体架构、技术路线、模块边界
Module Designer  负责模块设计、接口、数据流、验收标准
Developer        负责按设计实现代码
Tester           负责测试、验收、bug 记录
Adviser          负责解释、问答、辅助理解材料
```

角色不是固定层级。一个 Agent 工作区可以兼任多个角色，也可以是 Adviser / Reviewer / Researcher 这类旁支辅助角色。

## 常见流程

```text
understand
-> architecture
-> module-design
-> implement
-> review
-> test
-> report / handoff
```

这是常见链路，不是强制串行流程。任务结构由用户或当前父级 Agent 决定。

```text
handoff.md = 当前 Agent 工作区的交接上下文
report.md  = 当前 Agent 工作区的回报结果
overview.md = 顶层任务总览和跨角色稳定共识
```

## 状态层结构

```text
state/
  tasks/
    <task-id>/
      overview.md
      <agent-workspace>/
        handoff.md
        report.md
        <child-agent-workspace>/
          handoff.md
          report.md
```

规则：

- 顶层任务目录 `state/tasks/<task-id>/` 只能在用户明确要求开启任务时创建。
- 每个 Agent 窗口必须定位或创建自己的 Agent 工作区。
- 工作区目录名表达角色组合和职责，例如 `01-architecture-module-login/`、`02-developer-login-api/`、`03-adviser-context/`。
- 父子关系由目录嵌套表达；同级目录表示并列或旁支。
- 默认不设全局 index，也不设 map；目录树就是索引。
- 任务完成后不强制移动目录；完成状态写入 `overview.md` 和相关 `report.md`。

## 最小启动步骤

1. 填写 `docs/project-overview.md`
2. 填写 `rules/project-config.md`
3. 读取 `rules/context-rules.md` 和 `rules/collaboration-rules.md`
4. 根据用户描述匹配或请示创建顶层任务目录
5. 读取该任务的 `overview.md`
6. 定位或创建当前 Agent 工作区
7. 读取当前工作区的 `handoff.md` / `report.md` 和必要父子工作区
8. 需要架构时使用 `skills/architecture.md`
9. 需要模块设计时使用 `skills/module-design.md`
10. 需要实现时使用 `skills/implement.md`
11. 需要测试时使用 `skills/test.md`
12. 需要创建工作区、交接、回报或关闭时使用 `skills/handoff.md`

## 权威来源顺序

当信息冲突时，按以下顺序判断：

```text
用户最新明确指令
> docs/decisions/
> docs/architecture.md
> docs/module-map.md
> docs/modules/
> docs/implementation/
> docs/tests/
> state/tasks/<task-id>/overview.md
> 当前 Agent 工作区 report.md
> 当前 Agent 工作区 handoff.md
> 父级/子级相关工作区 report.md
> Adviser 的 derived context
```

如果冲突会影响实现、交接、回报或任务目录结构，必须先问用户。
