# 工作流 D：早晨规划

触发："早上好" / "开始规划" / "今天做什么"

1. 获取系统时间
2. 读 `$MEMORY_DATA/USER/behavior.md`（L3 行为规律 — 高效时段/精力模式）
3. 读 `$WORKSPACE/memory/MEMORY.md`（L4 当前目标/卡点）
4. 读 `$MEMORY_DATA/AGENTS/project-index.md`（项目总览）
5. 读昨日日记（`$MEMORY_DATA/USER/diary/YYYY/MM/YYYY-MM-DD.md`）结转未完成
6. 基于以上信息引导制定今日 P1/P2 目标（含 🍅 预估）
7. 创建今日日记文件（仅写 YAML frontmatter + SSOT 任务骨架，道痕部分晚间补）
8. 按 SKILL.md 日记模板输出

末尾追加标记：`[🧠 Agent-Memory: 早晨规划]` + `[🧠 路由: L4]`

执行完毕后，按 SKILL.md 通用推荐规则推荐下一步。
