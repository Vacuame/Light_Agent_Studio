# 活跃任务目录

每个活跃任务使用一个独立目录：

```text
state/tasks/active/<task-id>/
```

推荐最小结构：

```text
meta.md
progress.md
report.md
```

按需增加：

```text
handoff.md
links.md
children/
```

- `handoff.md`：向下交接，只有需要交给另一个角色、Agent 或子任务时才创建。
- `report.md`：向上回报，任务完成、阻塞、放弃或阶段结束时填写。
- `children/`：子任务目录，由用户或当前任务 owner 按需要创建。
