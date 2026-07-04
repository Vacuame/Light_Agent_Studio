# 质量门索引

质量门是关键产物交接前的检查点。

它不检查“角色本人”，而是检查“产物能不能交给下一个环节”。

## 读取原则

角色只需要读取自己当前任务相关的质量门，不需要读取所有质量门。

例如：

- Architect 只读 `rules/gates/architecture-gate.md`
- Developer 只读 `rules/gates/development-gate.md`
- Tester 只读 `rules/gates/test-gate.md`

## 质量门列表

| 质量门 | 适用场景 | 文件 |
|---|---|---|
| 管理门 | 修改规则、角色、技能、项目配置前 | `rules/gates/administration-gate.md` |
| 架构门 | 架构设计交给模块设计前 | `rules/gates/architecture-gate.md` |
| 模块门 | 模块设计交给开发前 | `rules/gates/module-gate.md` |
| 开发门 | 代码交给测试前 | `rules/gates/development-gate.md` |
| 测试门 | 任务关闭前 | `rules/gates/test-gate.md` |
| 顾问产物门 | Adviser 写入供其他 Agent 阅读的文件前 | `rules/gates/adviser-output-gate.md` |

## 结论格式

所有质量门统一使用以下结论：

```text
PASS：可以交接或修改
CONCERNS：可以继续，但必须记录风险
BLOCKED：不能继续，必须先补充或修正
```
