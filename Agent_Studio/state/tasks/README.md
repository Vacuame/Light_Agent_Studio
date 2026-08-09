# 轻量树形任务目录

`state/tasks/` 下每个顶层文件夹代表一个用户明确开启的任务。

Agent 不得自行创建顶层任务目录。如果当前工作需要任务目录但不存在，必须请示用户。

## 推荐结构

```text
state/tasks/<task-id>/
  overview.md
  <agent-workspace>/
    handoff.md
    report.md
    <child-agent-workspace>/
      handoff.md
      report.md
```

## overview.md

顶层任务总览，记录：

- 任务目标
- 背景
- 当前进展
- 重要文件
- 疑点
- 用户确认过的共识
- 影响后续 Agent 的稳定结论

`overview.md` 不是日志，也不是所有 report 的汇总。子级 Agent 写自己的 `report.md`；父级或汇总者读取 report 后，只把跨角色、稳定、会影响后续工作的结论写入 `overview.md`。

## Agent 工作区

每个 Agent 窗口必须定位或创建自己的工作区。工作区目录名应表达角色组合和职责，例如：

```text
01-architecture-module-login/
02-developer-login-api/
03-adviser-context/
04-reviewer-security/
```

角色可以组合，目录名不依赖固定角色枚举。

## 父子与旁支

- 嵌套目录表示父子关系。
- 同级目录表示并列关系或旁支辅助关系。
- Adviser、Reviewer、Researcher 这类辅助角色可以和主链节点并列，也可以挂在某个局部分支下。

## handoff.md

`handoff.md` 是给当前工作区的交接上下文，通常由父级或上游创建当前工作区时写入。

它应说明交接来源、本工作区职责、必读文件、已确认内容、临时假设、风险和下一步。

## report.md

`report.md` 是当前工作区向父级、上层或用户的回报。

它应说明本工作区结论、完成内容、修改或产出文件、验证结果、未完成项、风险、建议写入 overview.md 的稳定结论和建议下一步。
