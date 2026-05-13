# 工作流 H：进度记账 / Session 日志

触发："开始专注" / "完成" / "记账" / 对话结束自动

1. 用户报告进度 → 更新日记 SSOT 的"实际"列（番茄/状态）
2. 写工作区日志（追加到 `$WORKSPACE/memory/YYYY-MM-DD.md`，按 SKILL.md Session 日志模板）
3. 检查是否需要更新 L4：
   - 状态有变化 → 更新 `$WORKSPACE/memory/MEMORY.md`
   - 无变化 → 跳过
4. 检查是否需要更新项目总览：
   - 项目进展有变化 → 更新 `$MEMORY_DATA/AGENTS/project-index.md`
   - 无变化 → 跳过
5. 简短确认（一句话），不打断心流

末尾追加标记：`[🧠 Agent-Memory: 进度记账]` + `[🧠 路由: L4]`

执行完毕后，按 SKILL.md 通用推荐规则推荐下一步。
