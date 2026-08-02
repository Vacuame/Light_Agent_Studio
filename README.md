# My Agent Studio

这是一个轻量级 Agent 工作流框架，用来把一个通用 AI 助手拆成几个清晰角色，并通过文件完成协作、交接、记忆和质量检查。

## 核心思路

```text
规则层：规定怎么工作
角色层：规定谁来工作
技能层：规定某类任务怎么做
状态层：记录全局任务面板、任务索引、任务目录、交接和回报
产物层：保存已经确认的项目事实
质量门：决定关键产物能不能交接、回报或关闭
自动护栏：提醒、检查、防止忘记重要步骤
```

## 常见工作流

Agent Studio 支持按任务需要裁剪流程。常见链路是：

```text
理解项目 -> 架构设计 -> 模块设计 -> 程序实现 -> 审查 -> 测试 -> 回报/交接/关闭
```

这不是强制串行流程。任务结构、角色分配和是否拆分子任务由用户或当前任务 owner 决定。一个 Agent 可以兼任多个角色，一个任务也可以没有子任务。

对应技能：

```text
/start
/understand
/architecture
/module-design
/implement
/review
/test
/handoff
```

## 启动提示词

把 `Agent_Studio` 放入某个项目后，可以在新会话中直接复制这段话：

```text
你现在在这个项目中工作。

请先阅读：
1. Agent_Studio/rules/rules.md
2. Agent_Studio/overview.md
3. Agent_Studio/state/active.md
4. Agent_Studio/state/tasks/index.md

然后按 rules 中定义的 /start 启动流程开始。

启动后请告诉我：
1. 当前全局任务状态是什么
2. 当前是否已有聚焦任务
3. 如果已有聚焦任务，对应任务目录是什么
4. 如果没有聚焦任务，是否需要创建新任务目录
5. 缺少哪些项目信息或任务信息
6. 建议由哪个角色接手
7. 建议使用哪个 skill
8. 下一步需要我确认什么

规则、状态、角色、skill、质量门和产物的读取顺序全部由 rules 决定。

未经我确认，不要修改项目代码、状态层或产物层。
如果当前任务目录不明确，必须先向我确认，不要自行猜路径。
不要查找或写入全局 state/handoff.md；新版 handoff.md 只存在于具体任务目录中，表示向下交接。
任务完成、阻塞、放弃或阶段结束时，用具体任务目录中的 report.md 向上回报。
```

## 日常角色提示词

如果你想在日常使用中让 Agent 以某个已有角色接手，可以复制这段话，并把角色名和任务换成你需要的内容：

```text
你现在是 [角色名]。

请先阅读：
1. Agent_Studio/rules/rules.md
2. Agent_Studio/agents/[对应角色文件].md
3. Agent_Studio/state/active.md
4. Agent_Studio/state/tasks/index.md

然后按 rules 中定义的角色、skill、状态层和质量门流程开始工作。

本次任务：
[写清楚你要它做什么]

当前任务目录：
[如果已知，写 Agent_Studio/state/tasks/active/<task-id>/]
[如果未知，写：未知，请先根据 active.md 和 tasks/index.md 定位；仍不明确时向我确认]

如果当前任务目录存在，请读取其中：
- meta.md
- progress.md
- handoff.md，如果存在
- report.md，如果存在
- links.md，如果存在

请先告诉我：
1. 你理解的任务是什么
2. 你当前接手的是哪个任务目录
3. 你当前角色需要读取哪些项目文件
4. 是否缺少关键信息
5. 是否需要 handoff.md
6. 完成或阶段结束时 report.md 应该回报给谁
7. 你的下一步计划

未经我确认，不要修改项目代码、状态层或产物层。
如果 rules 没有告诉你下一步该读取什么，先向我确认，不要自行猜路径。
不要查找或写入全局 state/handoff.md；交接写具体任务目录中的 handoff.md，回报写具体任务目录中的 report.md。
```

常用对应关系：

```text
Administrator：修改 Agent 架构、规则、角色、技能、项目配置
Architect：理解项目整体、判断架构、建立模块地图
Module Designer：拆模块、定义接口、数据流和验收标准
Developer：根据模块设计实现代码
Tester：测试、验收、记录 bug 和关闭建议
Adviser：回答问题、解释代码、在用户要求时整理辅助理解材料
```

如果你是想“新增一个从未定义过的角色”，不要直接让新角色工作，先用 Administrator：

```text
你现在是 Administrator。
我想为 Agent Studio 新增一个角色：[新角色名]。
请先阅读 rules/rules.md，并按 rules 中定义的管理流程评估这次角色变更。
先评估这个角色是否真的需要新增、会影响哪些规则和技能、建议放哪些职责边界。
未经我确认，不要创建或修改角色文件。
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
  全局任务面板、任务索引、任务目录、任务级 handoff/report、会话记录

docs/
  项目总览、架构、模块地图、模块设计、技术决策、实现记录、测试记录
```

## 使用原则

1. 开始任务前，先读 `Agent_Studio/rules/rules.md`，再按 rules 指引读取状态、角色、skill、质量门和产物文件。
2. 任务开始时先定位 `state/active.md`、`state/tasks/index.md` 和当前任务目录；当前任务目录不明确时先问用户。
3. 不清楚就问，不允许用猜测替代决策。
4. 临时信息、任务进展、交接和回报写到 `state/`。
5. 已确认的长期事实写到 `docs/`。
6. `handoff.md` 是任务级向下交接，`report.md` 是任务级向上回报；不要使用全局 `state/handoff.md`。
7. 关键交接、回报或关闭前必须过对应质量门。
8. 修改规则、角色、技能时，必须走 Administrator 和管理门。
