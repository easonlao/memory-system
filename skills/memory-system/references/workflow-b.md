# 工作流 B：健康检查

触发："检查记忆" / "记忆状态"

## B1：扫描 $MEMORY_DATA 结构
检查：
- USER/core.md → 有内容/空/缺失
- USER/cognitive.md → 有内容/空/缺失
- USER/behavior.md → 有内容/空/缺失
- AGENTS/GL1-rules.md → 有内容/空/缺失
- AGENTS/GL2-patterns.md → 有内容/空/缺失
- AGENTS/project-index.md → 有内容/空/缺失
- questionnaire.md → 存在/缺失

## B2：检查配置文件
- config.json → 存在/格式正确/路径有效

## B3：输出报告
- 🟢 全部就绪 → 静默完成
- 🟡 部分缺失 → 列出缺失项，询问是否修复
- 🔴 严重缺失 → 提示重新安装

末尾追加标记：`[🧠 Agent-Memory: 健康检查]` + `[🧠 路由: 系统]`

执行完毕后，按 SKILL.md 通用推荐规则推荐下一步。
