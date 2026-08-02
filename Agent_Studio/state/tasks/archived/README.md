# 归档任务目录

已完成或放弃但需要保留记录的任务移动到：

```text
state/tasks/archived/<task-id>/
```

归档任务应保留必要的：

```text
meta.md
progress.md
report.md
handoff.md
links.md
closeout.md
```

`closeout.md` 用于说明：

- 为什么归档；
- 关闭结论；
- 剩余风险；
- 是否通过相关质量门；
- 如果以后恢复，应从哪里继续。

删除任务目录前必须获得用户确认。删除或归档后必须同步更新 `state/tasks/index.md` 和 `state/active.md`。
