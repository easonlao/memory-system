# 工作流 I：记忆琥珀回滚

触发："回滚" / "恢复版本"

原则：从记忆琥珀恢复历史版本，覆盖当前文件。
注意：覆写操作属于 P3 高风险，需遵循 AGENTS.md 的 G13/G14 协议。

## I1：列出可用快照
1. 询问用户要回滚哪个文件：
   - `core.md` → 列出 `$MEMORY_DATA/.amber/USER/core/`
   - `cognitive.md` → 列出 `$MEMORY_DATA/.amber/USER/cognitive/`
   - `behavior.md` → 列出 `$MEMORY_DATA/.amber/USER/behavior/`
   - `GL1-rules.md` → 列出 `$MEMORY_DATA/.amber/AGENTS/GL1/`
   - `GL2-patterns.md` → 列出 `$MEMORY_DATA/.amber/AGENTS/GL2/`
2. 按日期排序，显示最近 5 个快照

## I2：用户选择
- 用户指定日期 → 读取对应快照文件
- 用户取消 → 退出

## I3：确认回滚
1. 输出快照内容摘要（前 10 行）
2. 询问用户确认："确定用此版本覆盖当前文件？"
3. 确认 → 覆盖当前文件
4. 输出回滚完成摘要

末尾追加标记：`[🧠 Agent-Memory: 琥珀回滚]` + `[🧠 路由: 系统]`

执行完毕后，按 SKILL.md 通用推荐规则推荐下一步。
