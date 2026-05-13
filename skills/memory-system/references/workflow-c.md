# 工作流 C：升级流程

触发："升级记忆系统"

原则：只替换系统文件，不动用户数据。

## C0：检测 $MEMORY_DATA（config.json 丢失时的兜底）
如果 config.json 不存在但用户说"升级"：
1. 扫描常见路径：`~/.memory-data`、`~/.config/memory-data`、`~/Documents/memory-data`
2. 找到已有数据目录 → 询问用户确认路径 → 重建 config.json
3. 未找到 → 告知用户需要重新配置（说"使用记忆系统"）

## C1：版本检测 + 自动更新
（保留原 skills CLI 更新逻辑，如果可用则使用；否则提示手动更新）

## C2：更新 assets 资源文件
1. 更新 `{skill_dir}/assets/AGENTS.md`
2. 更新 `{skill_dir}/assets/questionnaire.md`
3. 更新 `{skill_dir}/assets/report-template.md`
（注：实际通过技能更新机制完成）

## C3：更新题库（可选）
1. 比较 `$MEMORY_DATA/questionnaire.md` 与新版 `{skill_dir}/assets/questionnaire.md`
2. 有新增/修改题目 → 询问是否补答
3. 无变化 → 跳过

## C4：更新 config.json
更新版本号为 6.0.0，更新 last_used

## C5：健康检查 + 输出摘要
运行工作流 B（读取 references/workflow-b.md），输出升级摘要

不动的内容（不更新，不替换）：
- USER/core.md
- USER/cognitive.md
- USER/behavior.md
- AGENTS/GL1-rules.md
- AGENTS/GL2-patterns.md
- AGENTS/project-index.md

末尾追加标记：`[🧠 Agent-Memory: 升级完成]` + `[🧠 路由: 系统]`

执行完毕后，按 SKILL.md 通用推荐规则推荐下一步。
