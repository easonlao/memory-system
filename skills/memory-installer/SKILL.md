---
name: memory-installer
description: 记忆系统安装入口。首次使用引导安装：配置平台入口、安装技能、创建数据目录、问卷填充。也是健康检查入口：检测记忆系统完整性。当你需要在平台入口文件中写入记忆系统模板、安装子技能、或检查记忆系统状态时使用。如果用户提到"记忆""安装记忆""记忆系统"等词，应该使用此技能。
---

# 🧠 Agent-Memory 安装器

> 这是 Agent-Memory 的唯一安装入口。安装完成后，子技能（memory-assistant、monthly-calibration、workspace-memory）会自动就绪。
> 所有依赖文件位于 `{skill_dir}/references/`。

---

## 工作流 A：首次安装

> 当 `$MEMORY_DATA` 未设置时执行。安装全程引导用户操作。

### 步骤 1：配置平台入口

```
1. 询问用户：你用什么 AI 平台？
   ├── Claude Code   → 入口文件：.claude/CLAUDE.md
   ├── Cursor        → 入口文件：.cursorrules
   ├── Gemini CLI    → 入口文件：GEMINI.md
   ├── GitHub Copilot→ 入口文件：.github/copilot-instructions.md
   └── 其他          → 让用户指定入口文件路径

2. 读取 {skill_dir}/references/AGENTS.md 内容
   追加到用户平台入口文件（不存在则创建）

3. ⚠️ 如果找不到入口文件（用户选了"其他"且路径无效）：
   输出 AGENTS.md 全文，告知用户手动复制到平台配置文件
   后续每次对话通过调用本 Skill 作为入口
```

### 步骤 2：安装子技能

```
1. 确定平台 skills 目录路径
   ├── Claude Code → .claude/skills/
   └── 其他平台 → 询问用户 skills 目录位置

2. 复制子技能到 skills 目录：
   ├── memory-assistant      → {skills_dir}/memory-assistant/SKILL.md
   ├── monthly-calibration   → {skills_dir}/monthly-calibration/SKILL.md
   ├── workspace-memory      → {skills_dir}/workspace-memory/SKILL.md
   └── reading-assistant     → 询问用户是否安装，是则复制
```

### 步骤 3：设置运行时数据目录

```
1. 询问用户选择 $MEMORY_DATA 路径（记忆数据存放位置）
   建议：~/.memory-data/ 或云盘同步目录

2. mkdir -p $MEMORY_DATA/{USER,AGENTS}

3. 复制 {skill_dir}/references/questionnaire.md 到 $MEMORY_DATA/
   告知：这是唯一需要备份的目录，迁移时完整复制即可

4. 将 $MEMORY_DATA 路径写入平台入口文件顶部：
   $MEMORY_DATA = {用户路径}
   确保下次启动时 AI 能读取到该变量
```

### 步骤 4：问卷填充

```
引导用户逐部分回答 $MEMORY_DATA/questionnaire.md：

第一部分 核心层（Q1-Q7）→ 写入 USER/L1-core.md
第二部分 认知层（Q8-Q17）→ 写入 USER/L2-L3-rules.md（L2 节）
第三部分 行为层（Q18-Q23）→ 写入 USER/L2-L3-rules.md（L3 节）
第四部分 情境层（Q24-Q28）→ 附注记录
协作契约（Q31-Q33）→ L1-core.md 顶部

每答一题立即写入。Q29-Q30 保留辅助参考。
```

### 步骤 5：编译 GL1 + 生成报告

```
1. 读取 USER/L1-core.md → 编译初始规则 → 写入 AGENTS/GL1-rules.md

2. 按 {skill_dir}/references/report-template.md
   生成《Agent-Memory 洞察报告》
   输出到 $MEMORY_DATA/agent-memory-insight-report.md
```

### 步骤 6：完成

```
输出安装摘要：
- 平台入口文件已配置
- X 个子技能已安装
- $MEMORY_DATA 路径已设置
- 各层数据已填充
- 报告已生成
```

---

## 工作流 B：健康检查

> `$MEMORY_DATA` 已知时，用户说"检查记忆"、"记忆状态"时执行。

```
1. 扫描 $MEMORY_DATA 结构
├── USER/L1-core.md          → 有内容/空/缺失
├── USER/L2-L3-rules.md      → 有内容/空/缺失
├── AGENTS/GL1-rules.md      → 有内容/空/缺失
├── AGENTS/GL2-patterns.md   → 有内容/空/缺失
├── AGENTS/project-index.md  → 有内容/空/缺失
└── questionnaire.md         → 存在/缺失

2. 扫描 skills 目录
├── memory-assistant     → 已安装/缺失
├── monthly-calibration  → 已安装/缺失
└── workspace-memory     → 已安装/缺失

3. 输出报告
🟢 全部就绪 → 静默完成
🟡 部分缺失 → 列出缺失项，询问是否修复
🔴 严重缺失 → 提示重新安装
```

---

## 工作流 C：升级系统

> 用户说"升级记忆系统"、"更新记忆系统"时执行。
> **原则：只替换系统文件，不动用户数据。**

```
1. 确认 $MEMORY_DATA 路径已知（保护用户数据）

2. 更新入口文件
   ├── 重新读取 {skill_dir}/references/AGENTS.md
   ├── 与现有入口文件中的版本对比
   └── 有变化 → 提示用户手动替换入口文件内容

3. 更新子技能
   ├── 找出 skills 目录中已有技能
   ├── memory-assistant → 覆盖（如果已安装）
   ├── monthly-calibration → 覆盖（如果已安装）
   ├── workspace-memory → 覆盖（如果已安装）
   └── reading-assistant → 询问是否新安装

4. 更新题库
   ├── 比较 $MEMORY_DATA/questionnaire.md 与新版
   └── 有新增/修改题目 → 询问是否补答

5. 运行健康检查确认安装后状态
   └── 输出升级摘要
```

**不动的内容**（不更新，不替换）：
- USER/L1-core.md
- USER/L2-L3-rules.md
- AGENTS/GL1-rules.md
- AGENTS/GL2-patterns.md
- AGENTS/project-index.md

---

## 执行标记

末尾追加标记标识记忆系统行为：
`[🧠 Agent-Memory: memory-installer - {安装/检查/升级}]`
