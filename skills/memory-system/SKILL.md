---
name: memory-system
description: Agent-Memory 一体化个人记忆系统。单文件夹复制即用，无需配置平台入口文件。包含安装、日记（道痕六层+石头追踪）、早晨规划、晚间复盘、周报整理、月度校准、进度记账、记忆琥珀回滚、健康检查、升级等完整工作流。当用户提到任何与个人记忆、日记、规划、复盘、周报、月总结、自我认知、习惯追踪、行为分析相关的内容时，都应该使用这个技能。即使是简单的"早上好"、"今天该做什么"、"写日记"、"检查记忆"、"MS-HELP"等日常用语也需要触发——不要等到用户明确说"使用记忆系统"才激活，只要对话涉及个人管理、时间规划、自我反思，就自动加载记忆系统。
---

# 🧠 Agent-Memory 一体化系统

> **全局最高准则：**
> 1. 格式即法律：严格遵循输出模板
> 2. 绝不造假：没有数据就留空
> 3. 文件唯一性：每天只能有 1 个日记文件
> 4. 路径正确性：日记走 `$MEMORY_DATA/USER/diary/`，工作区日志走 `{workspace}/memory/`（自动适配平台已有 memory 目录），不混淆
> 5. 时间真相：所有时间戳通过 `date` 命令获取
> 6. 复盘真相源：基于实际完成数据，禁止用计划数据
> 7. 记忆琥珀：覆写 USER/core.md、cognitive.md、behavior.md、AGENTS/GL1-rules.md、GL2-patterns.md 前，必须先备份到 `$MEMORY_DATA/.amber/`，保留最近 5 个版本
> 8. 冲突检测：执行文件操作前输出 `[冲突自检]`，🔴🟠 级冲突必须暂停确认
> 9. 深度推理：非 trivial 任务启用 G13 深度推理协议（理解→拆解→多路径思考→执行→验证），P3 高风险操作必须先呈现再确认
> 10. 路由签名：每条回复末尾追加 `[🧠 Agent-Memory: 工作流名]` + `[🧠 路由: 层级]`，忘记=系统故障

---

## 入口路由

### 步骤 0：配置检查
1. 检查 `{skill_dir}/config.json`
   - 不存在 → 读取 `references/workflow-a.md` 执行安装
   - 存在 → 读取 `memory_data_path` 并设置为 `$MEMORY_DATA`
     - 路径有效 → 进入已激活模式
     - 路径无效 → 询问用户重新配置

### 步骤 1：启动流程
参考 `assets/AGENTS.md` 执行启动流程：
- 检查 $MEMORY_DATA
- pwd → $WORKSPACE
- L4 自动适配（检查 $WORKSPACE/memory/）
- 读取 L4 MEMORY.md + 最近日志
- 读取 GL1（`$MEMORY_DATA/AGENTS/GL1-rules.md`）
- 读取 GL2（`$MEMORY_DATA/AGENTS/GL2-patterns.md`）
- 时间自检 + 出题自检

### 步骤 2：信号词路由

匹配到工作流后，先读取对应 `references/workflow-*.md` 的完整指令，再按步骤执行。

| 信号词 | 路由 | 读取文件 |
|--------|------|----------|
| "安装记忆系统" / "重新配置" | 工作流 A | `references/workflow-a.md` |
| "检查记忆" / "记忆状态" | 工作流 B | `references/workflow-b.md` |
| "升级记忆系统" | 工作流 C | `references/workflow-c.md` |
| "回滚" / "恢复版本" | 工作流 I | `references/workflow-i.md` |
| "MS-HELP" / "帮助" | 工作流 J | `references/workflow-j.md` |
| "早上好" / "开始规划" / "今天做什么" | 工作流 D | `references/workflow-d.md` |
| "今日复盘" / "晚间总结" / "写日记" | 工作流 E | `references/workflow-e.md` |
| "写周报" / "周复盘" | 工作流 F | `references/workflow-f.md` |
| "月度校准" / "月总结" / "本月回顾" | 工作流 G | `references/workflow-g.md` |
| "开始专注" / "完成" / "记账" | 工作流 H | `references/workflow-h.md` |
| "完成任务" / "收工" / 工作结束 | 工作流 H（含 project-index 同步） | `references/workflow-h.md` |
| 其他 | 日常对话（保持激活） | — |

---

## 推荐下一步

每个工作流执行完毕后，根据用户数据状态自动推荐：

| 数据状态 | 推荐内容 |
|---------|----------|
| 今日未写日记 | "今天还没有记录，要不要写日记？" |
| 本周未写周报且已是周末 | "本周还没写周报，要不要整理一下？" |
| 本月未校准且已是下旬 | "本月还没做月度校准，要不要跑一次？" |
| L4 超过 3 天未更新 | "当前工作区记忆超过 3 天没更新了，要不要更新？" |
| 一切正常 | "一切正常。有需要随时找我。" |

---

## 石头定义

石头是道痕六层剖析后露出的**底层驱动力**。

| 范畴 | 本质 | 模板句 |
|------|------|--------|
| **贪婪** | 想得到但还没得到的 | 我想______ |
| **恐惧** | 怕发生或怕已经发生的 | 我怕______ |

**关键规则：**
1. 每天只捞**一块主石头**（第六层结论），记录在当日日记 `stones` 字段
2. 每周回顾对比：同一石头反复出现 → 引发自我反思，不自动晋升
3. 月度校准时由 AI 综合分析全部日记数据（道痕层、SSOT、情绪、石头重复模式）后，系统性提取行为规律到 L3
4. 石头本身不写入 L3——石头是驱动力，L3 是行为规律，不混淆

---

## 数据路径参考

| 域 | 路径 | 说明 |
|----|------|------|
| L1 | `$MEMORY_DATA/USER/core.md` | 价值观/底线/驱动力 |
| L2 | `$MEMORY_DATA/USER/cognitive.md` | 认知模式 |
| L3 | `$MEMORY_DATA/USER/behavior.md` | 行为规律（含石头追踪） |
| 日记 | `$MEMORY_DATA/USER/diary/YYYY/MM/YYYY-MM-DD.md` | 个人日记 |
| 周记 | `$MEMORY_DATA/USER/diary/YYYY/MM/YYYY-Www.md` | 周汇总 |
| 月度日志 | `$MEMORY_DATA/USER/diary/YYYY/MM/monthly-log.md` | 月度校准总结 |
| L4 | `{workspace}/memory/MEMORY.md` | 当前状态快照（自动适配平台） |
| 工作区日志 | `{workspace}/memory/YYYY-MM-DD.md` | session 记录 |
| 项目总览 | `$MEMORY_DATA/AGENTS/project-index.md` | 跨项目索引 |
| 配置文件 | `{skill_dir}/config.json` | Skill 配置 |
| 记忆琥珀 | `$MEMORY_DATA/.amber/` | 备份版本快照 |

> **L4 自动适配规则：** 启动时检查 $WORKSPACE 下是否存在 memory 子目录。
> - 存在 → 使用平台的 memory 目录
> - 不存在 → 创建 memory/ 目录

---

## 输出模板

### 日记模板
```markdown
---
date: YYYY-MM-DD
day_of_week: Monday
tags: [memory-assistant, diary]
stones: [主石头名]
---

# YYYY-MM-DD 日记

## 1. SSOT 数据

| 维度 | 数据 |
|------|------|
| 入睡 | HH:MM |
| 起床 | HH:MM |
| 睡眠时长 | Xh |
| 总番茄 | X🍅 |
| 情绪评分 | X/10 |

## 2. 今日任务

| 优先级 | 目标 | 预计 | 实际 | 状态 |
|--------|------|------|------|------|
| P1 | {目标} | {X}🍅 | {X}🍅 | {✅/⏳/❌} |

## 3. 道痕

### 事实
{只写发生了什么，不评价不抒情}

### 第一反应
{最直接的感觉，不是正确答案}

### 贪婪 — 我想得到什么
{具体的欲望}

### 恐惧 — 我在害怕什么
{具体的恐惧}

### 自洽 — 我给了自己什么理由
{怎么消化这件事的}

### 主石头
{贪婪/恐惧 + 具体描述}

### 人选练习
{如果明天再遇到同样的事，怎么选}
```

### Session 日志模板（追加到 `$WORKSPACE/memory/YYYY-MM-DD.md`）
```markdown
# 工作日志 - YYYY-MM-DD
工作区: {$WORKSPACE}

## Session {序号} {HH:MM}
- 主题：{主要话题}
- 关键产出：{代码/方案/文档/决策}
- 待办：{未完成需要下次继续的事项}
```

### L4 MEMORY.md 模板（`$WORKSPACE/memory/MEMORY.md`）
```markdown
# 工作区记忆

类型: {项目/日常}
路径: {$WORKSPACE}

## 当前状态
- 项目：{项目名}
- 目标：{当前核心目标}
- 进展：{最近完成的关键事项}
- 卡点：{当前卡住的问题}

## 关键记录
- 决策：{已确定的方案}
- 上下文：{分支/配置/环境信息}

---
最后更新: {YYYY-MM-DD}
```

### 项目总览模板（`$MEMORY_DATA/AGENTS/project-index.md`）
```markdown
# 项目总览

| 工作区路径 | 类型 | 描述 | 最后更新 |
|------------|------|------|----------|
| {path} | {项目/日常} | {一句话描述} | {YYYY-MM-DD} |
```
