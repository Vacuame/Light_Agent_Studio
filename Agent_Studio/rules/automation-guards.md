# 自动护栏

自动护栏是提醒和机械检查，不代替用户判断。

当前版本先写规则，不实现脚本。

## 会话开始提醒

开始新会话时，应提醒读取：

```text
state/active.md
state/tasks/index.md
rules/project-config.md
```

如果已经确定要接手的任务，还应读取该任务目录下的：

```text
meta.md
progress.md
handoff.md   # 如果存在
report.md    # 如果存在
links.md     # 如果存在
```

## 压缩前保存

压缩或长任务中断前，应提醒更新：

```text
state/active.md
state/tasks/index.md
state/tasks/active/<task-id>/progress.md
```

必要时更新：

```text
state/tasks/active/<task-id>/handoff.md
state/tasks/active/<task-id>/report.md
```

## 危险操作提醒

以下操作前必须确认：

- 删除文件
- 删除任务目录
- 归档或移动任务目录
- 大规模移动目录
- 修改项目配置
- 修改规则、角色、技能
- 引入新依赖
- 重写架构

## 角色越界提醒

当前窗口必须遵守启动时声明的角色边界。

如果当前角色是 Architect、Module Designer，或“架构+模块”组合角色：

- 不得修改项目代码、配置、资源、测试代码或构建脚本。
- 不得为了验证自己改动而运行构建或测试。
- 不得把用户描述的功能需求当作实现授权。
- 只能输出设计、影响范围、验收标准和给 Developer 的 handoff。

当设计角色准备写入源码、配置、资源、测试、脚本或构建配置时，必须停止并提示：

```text
当前角色不允许修改项目代码。
请确认是否切换到 Developer 并开始实现。
```

## 步骤进展提醒

每个阶段完成前，需要用户确认。

用户确认后，才可以：

- 更新当前任务目录下的 `handoff.md`
- 更新当前任务目录下的 `report.md`
- 更新正式产物
- 标记当前阶段完成
- 更新 `state/tasks/index.md` 和 `state/active.md`

## 状态陈旧提醒

如果 `state/active.md`、`state/tasks/index.md` 或当前任务目录明显不一致，应先更新状态，再继续任务。

常见情况：

- `active.md` 记录的是旧任务
- `active.md` 指向的任务目录不存在
- `tasks/index.md` 记录的路径不存在
- 任务目录存在但没有登记到 `tasks/index.md`
- `handoff.md` 指向不存在的下一步
- `report.md` 写了完成，但任务索引仍是 active
- docs 已更新但 active.md 未更新
- 测试失败但任务状态仍写“完成”

## 任务目录一致性提醒

更新任务目录时，提醒检查：

- 是否有 `meta.md`
- 是否有 `progress.md`
- 闭环时是否有 `report.md`
- 有交接时是否有 `handoff.md`
- 如果有子任务，父任务是否链接了子任务
- 删除或归档后，`active.md` 和 `tasks/index.md` 是否仍残留旧路径

## 正式产物写入提醒

写入 `docs/` 前，提醒检查：

- 是否已经用户确认？
- 是否是长期事实？
- 是否通过对应质量门？
- 是否需要同步更新其他产物？

## Git 提交

当前不做提交前自动检查。

用户手动提交更安全。

## 未来可选脚本

以后如果需要自动化，可以增加：

- 会话开始时打印 `state/active.md` 和 `state/tasks/index.md`
- 压缩前提醒更新当前任务目录
- 写入 `docs/` 前提醒检查质量门
- 检查任务索引中的路径是否存在
- 检查 TODO/FIXME 是否有说明
