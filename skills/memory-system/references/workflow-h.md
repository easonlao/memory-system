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
5. **GL2c → GL2b 提炼**：回顾本对话中所有 `GL2c#{序号}` 标记，与已存的 `$WORKSPACE/memory/.rules/` 去重后，逐条询问用户："提炼规则：{GL2c#N 描述}，要写入项目规则吗？"
   - 用户确认 → 写入 `.rules/` 对应文件
   - 用户拒绝 → 跳过
   - 无 GL2c# 标记 → 跳过
6. **AI 观察模式衰减**（今日无晚间复盘或月度校准时才执行）：
   - 检查今日日记文件末尾是否有 `[🧠 Agent-Memory: 晚间复盘]` 或 `[🧠 Agent-Memory: 月度校准]` 标记
     - 有 → 跳过衰减（已强化）
     - 无 → 读取 `$MEMORY_DATA/.last_decay_check`
       - 同一天 → 跳过
       - 不同日期 → 读取 behavior.md 和 cognitive.md 中置信度 < 0.7 且非问卷来源的 AI 观察模式，每项 -0.1，< 0.3 移入历史区
       - 写入 `$MEMORY_DATA/.last_decay_check` = 今天日期
7. 简短确认（一句话），不打断心流

末尾追加标记：`[🧠 Agent-Memory: 进度记账]` + `[🧠 路由: L4]`

执行完毕后，按 SKILL.md 通用推荐规则推荐下一步。
