# 上下文规则

本文件是状态层结构、上下文恢复和状态文件格式模板的唯一权威来源。

handoff/report 的方向、写入位置和确认机制见 `rules/collaboration-rules.md`。全局原则见 `rules/rules.md`。

## 核心原则

文件是长期记忆，对话只是临时过程。

重要信息不要只留在聊天里。只要会影响后续工作，就要考虑写入 `state/` 或全局 `docs/`；但 `handoff.md`、`report.md`、任务级 `docs/*.md` 和正式 `docs/` 都必须按各自确认规则，在用户明确要求或确认后才写入。

```text
state/ = 当前怎么接着干
state/<task-id>/docs/ = 用户授权后的任务级公共认知草稿
全局 docs/ = 已确认的项目事实
```

## 状态层组织

状态层采用轻量树形任务工作区：

```text
state/<task-id>/
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

说明：

- `state/<task-id>/` 是用户明确开启的顶层任务目录。
- `overview.md` 是顶层任务总览，记录任务背景、目标、当前进展、重要文件、疑点、共识和会影响后续 Agent 的稳定结论。
- `docs/` 是任务级公共认知区，按用户要求创建或修改其中的 Markdown 文件，记录任务推进中产生、多个 Agent 需要共享、但暂时不适合写入全局 `docs/` 的发现、假设、疑点、候选决策和参考线索。
- `<agent-workspace>/` 是某个 Agent 窗口的工作区，每个 Agent 窗口都必须定位或创建自己的工作区。
- `handoff.md` 是写给当前工作区的交接。
- `report.md` 是当前工作区写出的回报。
- 嵌套工作区表示父子关系；同级工作区表示并列或旁支关系。关系判断见 `rules/collaboration-rules.md`。
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

子级 Agent 写 `report.md` 时不自动更新 `overview.md`。是否更新、谁更新、如何确认，见 `rules/collaboration-rules.md`。

## 任务级 docs/

`state/<task-id>/docs/` 是任务内公共认知草稿区。只有用户明确要求维护任务级公共认知，或用户确认当前任务需要任务级 docs 时，才按需创建或修改其中的 Markdown 文件；Agent 不得自行判断并创建或写入任务级 docs。

它适合记录：

- 任务推进中新发现的代码结构、调用链、配置、限制或异常现象
- 多个 Agent 都需要知道，但尚未确认到可以写入全局 `docs/` 的事实候选
- 暂时采用的假设
- 需要用户、父级 Agent 或后续 Agent 确认的问题
- 候选决策、备选方案和参考线索

它不适合记录：

- 单个 Agent 的完整工作过程
- 完整 `handoff.md` 或 `report.md`
- 已确认的长期项目事实
- 普通聊天流水账

写入任务级 `docs/` 下的 Markdown 文件时必须标明：

```markdown
## 条目标题

来源：
确定性：高 / 中 / 低
影响范围：
内容：
待确认问题：
建议后续处理：
```

维护规则：

- 用户已授权任务级 docs 后，Agent 可以把会影响多个 Agent 的任务内信息追加到合适的 Markdown 文件中；如果没有合适文件，先按内容命名创建新的 Markdown 文件。
- 不确定内容必须标明确定性，不得写成已确认事实。
- 父级、汇总者或任务 owner 可以整理、去重、改写过期条目，但写入前仍按协作规则确认。
- 内容被用户确认并具有长期价值后，再提升到全局 `docs/`。
- 内容已经过期或被否定时，保留简短说明，不要无痕删除。

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

如果会话将被压缩或任务很长，当前 Agent 应提醒用户是否需要把上下文保存到状态层通信文件；用户确认后再写入。

需要保存时，优先说明：

- 已经做完什么
- 还没做什么
- 哪些文件是权威来源
- 下个角色或上层 owner 应该从哪里继续
- 当前顶层任务目录和 Agent 工作区路径

具体写入 `handoff.md`、`report.md` 或 `overview.md` 的方向和确认机制见 `rules/collaboration-rules.md`。

## 压缩后

压缩或换窗口后，第一步必须读取：

1. 当前顶层任务的 `overview.md`
2. 当前 Agent 工作区的 `handoff.md`（如果存在）
3. 当前 Agent 工作区的 `report.md`（如果存在）
4. 必要的父级、子级或兄弟工作区 `report.md`
5. 用户已授权且当前任务相关的任务级 `docs/*.md`
6. 当前任务相关的正式产物文件

不要根据压缩摘要直接继续做复杂决策。

## 上下文污染控制

状态层只记录后续继续工作真正需要的信息。

`overview.md`、任务级 `docs/*.md`、`handoff.md` 和 `report.md` 应优先记录：

- 已确认事实
- 当前进展
- 当前阻塞
- 当前最小下一步
- 需要用户或上层 owner 判断的问题
- 明确标注的临时假设

不要把未经确认的完整方案、假想任务树、完整下游流程或被用户否定的长方案全文写入状态层。遇到不确定点时，先记录当前阻塞或待确认问题，不要带着未确认前提继续扩展状态内容。

## 结论修订

已写入状态层或产物层的结论被推翻时，不静默修改。在原处保留修订记录：旧结论、新结论、推翻原因、依据、日期。

## handoff 与 report 格式模板

`handoff.md` 和 `report.md` 只是 Agent 之间的工作交流文件，不是状态机、流程引擎或阶段判定器。

方向、位置和写入确认见 `rules/collaboration-rules.md`。

### handoff.md 推荐格式

```markdown
# 任务交接

## 交接来源

## 交接给谁

## 接手什么

## 必读文件

本节只写当前交接任务的直接输入，例如任务上下文、上游交接、正式产物、源码、测试记录或状态文件；不要写通用启动、角色装配、skill、质量门或项目配置清单。

## 已确认内容

条目化。每条：结论 + 依据（文件:行 / 命令 / 测试 / 用户指令）+ 确定性（高/中/低）。标注规则见 rules/rules.md 结论纪律。未亲自核实的细节（含落点涉及的链路行为、既有机制）必须归入临时假设或标注核实状态，不得写成已确认内容；接手 Agent 对 handoff 内容的信任等级见 rules/collaboration-rules.md。

## 临时假设

## 风险

## 实现落点摘要

## 下一步
```

### report.md 推荐格式

```markdown
# 工作区回报

## 回报给谁

## 本工作区结论

PASS / CONCERNS / BLOCKED / DROPPED

只评价当前回报内容或当前工作区职责，不评价整个顶层任务，除非当前工作区就是顶层汇总者并且已经读取必要的下级 report。

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

Adviser 写文件的质量要求见 `rules/gates/adviser-output-gate.md`；需要起草辅助理解材料时，可按需使用 `skills/templates/derived-context-template.md`。

## 长任务更新频率

长任务不需要每一步都更新正式产物；需要留痕时，先询问用户是否写入状态层通信文件。

建议：

- 需要留下阶段结论、阻塞或下一步时，询问是否写当前 Agent 工作区的 `report.md`。
- 需要另一个 Agent 接续时，询问是否在接手工作区写 `handoff.md`。
- 父级、汇总者或任务 owner 读取 report 后，询问是否更新顶层任务 `overview.md`。
- 每次用户确认长期结论，再更新全局 `docs/`。

## 状态层与产物层

```text
state/ = 当前怎么接着干
state/<task-id>/docs/ = 用户授权后的任务级公共认知草稿
全局 docs/ = 已确认的项目事实
```

如果只是临时进度、阻塞、下一步、交接或回报，写入 `state/`。

如果是长期会被后续角色依赖的事实，写入全局 `docs/`。
