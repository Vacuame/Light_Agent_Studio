# Agent Studio CN 内部导览

这是一个轻量级、通用型 Agent 工作流框架。

它的目标不是模拟一个大型组织，而是把常见 AI 协作流程拆成少数稳定角色，让 Agent 在多轮任务中不丢上下文、不乱改边界、不把临时判断当成长期事实。

## 核心分层

```text
规则层：规定怎么工作
角色层：规定谁来工作
技能层：规定某类任务怎么做
状态层：记录任务目录、进展、交接和回报
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

## 默认流程

```text
understand
-> architecture
-> module-design
-> implement
-> review
-> test
-> report / handoff
```

任务结构由用户或当前任务 owner 决定。框架不判断任务是大、中、小，也不强制完整架构-模块-程序-测试链路。

```text
handoff.md = 向下交接
report.md  = 向上回报
```

任务可以是单目录任务，也可以拆成多个子任务；一个 Agent 可以兼任多个角色。框架只要求交接、进展、回报、归档路径清楚，避免覆盖和丢上下文。

## 状态层结构

```text
state/
  active.md              全局任务面板
  tasks/index.md         任务索引
  tasks/active/<task-id>/
    meta.md              任务元信息
    progress.md          任务进展
    report.md            向上回报
    handoff.md           向下交接，按需存在
    links.md             相关链接，按需存在
    children/            子任务，按需存在
  tasks/archived/        归档任务
  session-log.md         重要历史摘要
```

## 最小启动步骤

1. 填写 `docs/project-overview.md`
2. 填写 `rules/project-config.md`
3. 读取 `state/active.md` 和 `state/tasks/index.md`
4. 选择或创建当前任务目录
5. 需要架构时使用 `skills/architecture.md`
6. 需要模块设计时使用 `skills/module-design.md`
7. 需要实现时使用 `skills/implement.md`
8. 需要测试时使用 `skills/test.md`
9. 需要交接、回报、关闭、归档或删除任务时使用 `skills/handoff.md`

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
> state/tasks/active/<task-id>/report.md
> state/tasks/active/<task-id>/handoff.md
> state/tasks/active/<task-id>/progress.md
> state/active.md
> Adviser 的 derived context
```

如果冲突会影响实现或交接，必须先问用户。
