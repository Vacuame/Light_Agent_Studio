# My Agent Studio CN

这是一个轻量级 Agent 工作流框架，用来把一个通用 AI 助手拆成几个清晰角色，并通过文件完成协作、交接、记忆和质量检查。

当前版本是中文人类可读版。以后可以在此基础上增加英文版，专门给 Agent 读取。

## 核心思路

```text
规则层：规定怎么工作
角色层：规定谁来工作
技能层：规定某类任务怎么做
状态层：记录现在做到哪
产物层：保存已经确认的项目事实
质量门：决定关键产物能不能交给下一环节
自动护栏：提醒、检查、防止忘记重要步骤
```

## 推荐工作流

```text
理解项目 -> 架构设计 -> 模块设计 -> 程序实现 -> 审查 -> 测试 -> 交接/关闭
```

对应技能：

```text
/understand
/architecture
/module-design
/implement
/review
/test
/handoff
```

## 目录说明

```text
rules/
  系统规则、上下文规则、协作规则、项目配置、质量门、自动护栏

agents/
  Administrator、Architect、Module Designer、Developer、Tester、Adviser

skills/
  每类任务的 SOP

state/
  当前进度、临时交接、会话记录

docs/
  项目总览、架构、模块地图、模块设计、技术决策、实现记录、测试记录
```

## 使用原则

1. 开始任务前，先读 `rules/rules.md`、`state/active.md` 和相关产物文件。
2. 不清楚就问，不允许用猜测替代决策。
3. 临时信息写到 `state/`。
4. 已确认的长期事实写到 `docs/`。
5. 关键交接前必须过对应质量门。
6. 修改规则、角色、技能时，必须走 Administrator 和管理门。

