# Skill: review

用于检查设计、架构或代码是否符合上游产物。

## 目标

- 找出偏离设计的地方
- 找出风险
- 判断能否交给下一环节

## 适用场景

- 模块设计交给开发前
- 代码交给测试前
- 规则或技能修改前

## 流程

1. 明确要 review 的对象。
2. 读取上游权威文件。
3. 根据 review 对象只读取对应质量门：
   - 规则/角色/技能变更：`rules/gates/administration-gate.md`
   - 架构产物：`rules/gates/architecture-gate.md`
   - 模块设计：`rules/gates/module-gate.md`
   - 代码实现：`rules/gates/development-gate.md`
   - 测试产物：`rules/gates/test-gate.md`
   - Adviser 辅助材料：`rules/gates/adviser-output-gate.md`
4. 对照对应质量门检查。
5. 输出问题列表。
6. 给出结论。

## 结论格式

```text
PASS：可以交接
CONCERNS：可以交接，但有风险
BLOCKED：不能交接，必须先修
```

## 输出

- review 摘要
- 风险列表
- 修改建议
