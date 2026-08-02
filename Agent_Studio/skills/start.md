# Skill: start

用于每次会话开始、首次把本框架放入项目、或上下文不确定时启动工作。

## 目标

- 建立当前会话的工作上下文
- 判断这次应该由哪个角色接手
- 判断应该使用哪个技能 SOP
- 检查状态层和项目配置是否足够继续
- 定位当前任务目录，或提示用户创建/选择任务
- 在用户确认前，不修改状态层、产物层或项目代码

## 输入

- 用户的启动请求
- 当前项目目录
- Agent Studio 所在目录

如果 Agent Studio 所在目录不明确，先询问用户，不要猜路径。

## 必读文件

- `overview.md`
- `rules/rules.md`
- `rules/context-rules.md`
- `rules/collaboration-rules.md`
- `rules/project-config.md`
- `rules/quality-gates.md`
- `rules/automation-guards.md`
- `state/active.md`
- `state/tasks/index.md`

如果已经确定当前任务目录，再读取该任务目录下的：

- `meta.md`
- `progress.md`
- `handoff.md`（如果存在）
- `report.md`（如果存在）
- `links.md`（如果存在）

如果用户给出了具体任务，再读取对应角色和技能：

- 修改 Agent 架构：`agents/administrator.md`、`skills/update-agent-system.md`
- 理解项目整体：`agents/architect.md`、`skills/understand.md`、`skills/architecture.md`
- 拆模块和任务：`agents/module-designer.md`、`skills/module-design.md`
- 实现代码：`agents/developer.md`、`skills/implement.md`
- 测试验收：`agents/tester.md`、`skills/test.md`
- 解释问题或整理材料：`agents/adviser.md`

## 流程

1. 确认 Agent Studio 根目录和项目根目录。
2. 读取启动必读文件。
3. 摘要全局任务面板：当前聚焦任务、活跃任务、阻塞任务、任务索引。
4. 如果用户指定任务，定位对应任务目录。
5. 如果任务目录不明确，列出可选任务或询问用户。
6. 检查 `rules/project-config.md` 是否已填写关键配置。
7. 判断本次任务类型：
   - Agent 架构调整 → Administrator
   - 项目整体理解或架构判断 → Architect
   - 模块拆解和接口设计 → Module Designer
   - 代码实现和修改 → Developer
   - 测试、验收、bug 复现 → Tester
   - 问答、解释、辅助理解材料 → Adviser
8. 判断需要使用的技能 SOP。
9. 列出下一步需要读取的文件。
10. 如果状态层缺失、过期或任务目录不存在，提出更新建议，但先征求用户确认。
11. 输出启动摘要和建议接手角色。

## 输出

启动完成后，给用户输出：

```text
启动摘要：
项目根目录：
Agent Studio 目录：
当前聚焦任务：
活跃任务：
阻塞任务：
当前任务目录：
当前状态：
缺失信息：
建议角色：
建议技能：
下一步需要读取：
是否需要更新 state/active.md 或 state/tasks/index.md：
等待用户确认：
```

## 首次放入项目时

如果这是第一次把 Agent Studio 放入某个项目，优先建议：

```text
Administrator -> Architect
```

Administrator 先检查规则、状态和配置是否可用；Architect 再建立项目总览、架构理解和模块地图。

首次初始化时，建议补齐：

- `rules/project-config.md`
- `docs/project-overview.md`
- `docs/module-map.md`
- `state/active.md`
- `state/tasks/index.md`

这些文件不要自动填写为事实。缺信息时先向用户提问，或把内容标为“待确认”。

## 禁止

- 不要在启动阶段直接修改项目代码。
- 不要在没有用户确认时更新正式产物。
- 不要把猜测写入 `docs/`。
- 不要跳过 `state/active.md` 和 `state/tasks/index.md`。
- 不要因为缺少配置就自行假设运行命令、测试命令或技术栈。
- 不要替用户判断任务应该拆成大/中/小结构；任务分配由用户或任务 owner 决定。
