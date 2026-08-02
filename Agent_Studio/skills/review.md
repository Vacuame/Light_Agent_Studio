# Skill: review

用于检查设计、架构、代码、交接或回报是否符合上游产物。

## 目标

- 找出偏离设计的地方
- 找出风险
- 判断能否交给下一环节、向上回报或关闭任务

## 适用场景

- 架构产物交给下游或向上回报前
- 模块设计交给开发或向上回报前
- 代码交给测试或向上回报前
- 测试结果支持关闭任务前
- 规则或技能修改前
- 任务级 `handoff.md` / `report.md` 写入前

## 流程

1. 明确要 review 的对象。
2. 明确对象所属任务目录。
3. 读取上游权威文件。
4. 读取当前任务目录下的相关状态文件。
5. 根据 review 对象只读取对应质量门：
   - 规则/角色/技能变更：`rules/gates/administration-gate.md`
   - 架构产物：`rules/gates/architecture-gate.md`
   - 模块设计：`rules/gates/module-gate.md`
   - 代码实现：`rules/gates/development-gate.md`
   - 测试产物：`rules/gates/test-gate.md`
   - Adviser 辅助材料：`rules/gates/adviser-output-gate.md`
6. 对照对应质量门检查。
7. 如果对象是 `handoff.md`，检查接手对象、必读文件、风险、下一步是否清楚。
8. 如果对象是 `report.md`，检查结论、完成内容、验证结果、风险、建议下一步是否清楚。
9. 输出问题列表。
10. 给出结论。

## 结论格式

```text
PASS：可以交接、回报或关闭
CONCERNS：可以继续，但有风险
BLOCKED：不能继续，必须先修
```

## 输出

- review 摘要
- 任务目录
- 风险列表
- 修改建议
- 建议结论
