# 顾问产物门

适用于检查 Adviser 写给其他 Agent 阅读的辅助材料。

结论格式见 `rules/quality-gates.md`。角色权限见当前 `agents/<role>.md`。

普通问答不需要读取本文件。只有 Adviser 要写 derived context 或长期参考材料时才需要。

## 适用交付物

- derived context
- 给其他 Agent 阅读的辅助理解文件
- 用户要求保存的非权威解释材料

## 使用时机

当 Adviser 辅助材料准备写入文件、并可能被其他 Agent 阅读或引用前使用。

## 检查清单

- 内容是否清晰易懂？
- 是否标明来源？
- 是否区分事实、推测、建议？
- 是否注明不是权威设计？
- 是否注明权威来源在哪里？
- 是否有过期风险？
- 是否会误导 Developer 或 Tester 把总结当成事实？

## 输出要求

写入文件前必须包含：

```text
重要声明：
权威来源：
事实：
推测：
建议：
过期风险：
建议结论：PASS / CONCERNS / BLOCKED
```
