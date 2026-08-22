# Agent Studio 内部导览

这是一个轻量级、通用型 Agent 工作流框架。

它的目标不是模拟一个大型组织，而是把常见 AI 协作流程拆成少数稳定角色，让 Agent 在多轮任务中不丢上下文、不乱改边界、不把临时判断当成长期事实。

## 核心分层

```text
规则层：规定全局原则、上下文、协作协议和项目配置
角色层：规定谁能做、职责和权限边界
技能层：规定某类任务怎么做
状态层：记录当前怎么接着干
产物层：保存已经确认的项目事实
质量门层：检查交付物能否交接、回报或支持关闭判断
自动护栏层：提醒、检查、防止忘记重要步骤
```

## 权威来源口诀

```text
全局原则看 rules/rules.md
上下文放哪看 rules/context-rules.md
怎么交接看 rules/collaboration-rules.md
谁能做看 agents/
怎么做看 skills/
做得够不够看 rules/quality-gates.md 和 rules/gates/
项目命令和依赖看 rules/project-config.md
提醒和护栏看 rules/automation-guards.md
```

不要在 overview 里复制完整规则。具体规则以对应权威文件为准。

## 默认角色

```text
Administrator    维护 Agent 架构本身
Architect        负责总体架构、技术路线、模块边界
Module Designer  负责模块设计、接口、数据流、验收标准
Developer        负责按设计实现代码
Tester           负责测试、验收、bug 记录
Adviser          负责解释、问答、辅助理解材料
Reviewer         负责对待审查结论做证伪审查（仅供子 Agent 使用）
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
-> handoff / report
```

这是常见链路，不是强制串行流程。任务结构由用户或当前任务 owner 决定。

## 状态层

状态层采用轻量树形任务工作区。完整结构、文件职责和格式模板见 `rules/context-rules.md`。

协作关系、handoff/report 方向、写入位置和确认机制见 `rules/collaboration-rules.md`。

## 最小启动步骤

1. 如果角色不明确，读取 `rules/rules.md`、`skills/start.md` 和本导览来判断或询问当前角色
2. 角色明确后，读取对应 `agents/<role>.md`
3. 按角色文件里的 `## 角色专属资源`，结合当前任务需要选择读取相关 skill、质量门、状态层文件和正式产物
4. 如果是组合角色，合并所有参与角色的角色专属资源，按当前任务需要去重读取；权限冲突时采用更严格权限
5. 按当前任务选择额外 skill 或质量门

## 冲突处理

规则冲突时先按 `rules/rules.md` 的权威来源判断；协作文件冲突时按 `rules/collaboration-rules.md` 处理。

如果冲突会影响实现、交接、回报或任务目录结构，必须先问用户。
