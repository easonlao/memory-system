---
name: memory-system
description: Agent-Memory 一体化记忆系统。单文件夹复制即用，包含安装、日常对话、日记、规划、月度校准等所有功能。
---

# 🧠 Agent-Memory 一体化系统

> **全局最高准则：**
> 1. 格式即法律：严格遵循输出模板
> 2. 绝不造假：没有数据就留空
> 3. 文件唯一性：每天只能有 1 个日记文件
> 4. 路径正确性：日记走 `$MEMORY_DATA/USER/diary/`，工作区日志走 `{workspace}/memory/`（自动适配平台已有 memory 目录），不混淆
> 5. 时间真相：所有时间戳通过 `date` 命令获取
> 6. 复盘真相源：基于实际完成数据，禁止用计划数据

---

## 入口路由

### 步骤 0：配置检查
1. 检查 `{skill_dir}/config.json`
   - 不存在 → 进入「工作流 A：安装流程」
   - 存在 → 读取 `memory_data_path` 并设置为 `$MEMORY_DATA`
     - 路径有效且目录存在 → 进入「已激活模式」
     - 路径无效或目录不存在 → 询问用户重新配置

### 步骤 1：执行启动流程
参考 `{skill_dir}/assets/AGENTS.md` 中的指导，执行以下启动流程：
- 检查 $MEMORY_DATA（已在步骤 0 确认）
- pwd → $WORKSPACE
- **L4 自动适配**：检查 $WORKSPACE 下是否存在 memory 子目录
  - 存在 → 使用该目录作为 L4 工作目录
  - 不存在 → 创建 memory/ 目录
- 检查 $WORKSPACE/memory/MEMORY.md → 存在则读取
- 检查 $WORKSPACE/memory/ 最近的 YYYY-MM-DD.md → 存在则读取
- 读取 GL1（$MEMORY_DATA/AGENTS/GL1-rules.md）
- 读取 GL2（$MEMORY_DATA/AGENTS/GL2-patterns.md）
- 时间自检（根据时间段 + 文件状态判定）
- 出题自检（根据记忆缺口判定是否需要追问）

### 步骤 2：信号词路由
根据用户意图，路由到对应工作流：

| 信号词 | 工作流 |
|--------|--------|
| "安装记忆系统" / "重新配置" | 工作流 A：安装流程 |
| "检查记忆" / "记忆状态" | 工作流 B：健康检查 |
| "升级记忆系统" | 工作流 C：升级流程 |
| "早上好" / "开始规划" / "今天做什么" | 工作流 D：早晨规划 |
| "今日复盘" / "晚间总结" / "写日记" | 工作流 E：晚间复盘 |
| "写周报" / "周复盘" | 工作流 F：周报整理 |
| "月度校准" | 工作流 G：月度校准 |
| "开始专注" / "完成" / "记账" | 工作流 H：进度记账 |
| 其他 | 日常对话（保持记忆系统激活） |

---

## 石头定义

石头是道痕六层剖析后露出的**底层驱动力**。

| 范畴 | 本质 | 模板句 |
|------|------|--------|
| **贪婪** | 想得到但还没得到的 | 我想______ |
| **恐惧** | 怕发生或怕已经发生的 | 我怕______ |

**关键规则：**
1. 每天只捞**一块主石头**（第六层结论）
2. 同一本质在不同事件中出现 3+ 次 → L3 行为规律候选
3. 持续 3 个月以上 → 月度校准中晋升 L2/L1

---

## 数据路径参考

| 域 | 路径 | 说明 |
|----|------|------|
| L1 | `$MEMORY_DATA/USER/core.md` | 价值观/底线/驱动力 |
| L2 | `$MEMORY_DATA/USER/cognitive.md` | 认知模式 |
| L3 | `$MEMORY_DATA/USER/behavior.md` | 行为规律（含石头追踪） |
| 日记 | `$MEMORY_DATA/USER/diary/YYYY/MM/YYYY-MM-DD.md` | 个人日记 |
| 周记 | `$MEMORY_DATA/USER/diary/YYYY/MM/YYYY-Www.md` | 周汇总（与日记同目录） |
| 月度日志 | `$MEMORY_DATA/USER/diary/YYYY/MM/monthly-log.md` | 月度校准总结 |
| L4 | `{workspace}/memory/MEMORY.md` | 当前状态快照（自动适配平台） |
| 工作区日志 | `{workspace}/memory/YYYY-MM-DD.md` | session 记录（自动适配平台） |
| 项目总览 | `$MEMORY_DATA/AGENTS/project-index.md` | 跨项目索引 |
| 配置文件 | `{skill_dir}/config.json` | Skill 配置 |

> **L4 自动适配规则**：启动时检查 $WORKSPACE 下是否存在 memory 子目录。
> - 存在 → 使用平台的 memory 目录
> - 不存在 → 创建 memory/ 目录

---

## 工作流 A：安装流程

**触发：** 首次使用（无 config.json）/ 用户说"安装记忆系统" / "重新配置"

### A1：配置 $MEMORY_DATA 路径
1. 询问用户选择 $MEMORY_DATA 路径（记忆数据存放位置）
   - 建议：~/.memory-data/ 或云盘同步目录
2. 验证路径有效性

### A2：创建目录结构
1. 创建：`$MEMORY_DATA/USER/`
2. 创建：`$MEMORY_DATA/AGENTS/`
3. 创建：`$MEMORY_DATA/USER/diary/`（预留）

### A3：复制题库
1. 复制 `{skill_dir}/assets/questionnaire.md` → `$MEMORY_DATA/questionnaire.md`
2. 告知用户：这是唯一需要备份的目录，迁移时完整复制即可

### A4：问卷填充
引导用户逐部分回答 `$MEMORY_DATA/questionnaire.md`：
- 第一部分 核心层（Q1-Q7）→ 写入 USER/core.md
- 第二部分 认知层（Q8-Q17）→ 写入 USER/cognitive.md
- 第三部分 行为层（Q18-Q23）→ 写入 USER/behavior.md
- 第四部分 情境层（Q24-Q28）→ USER/behavior.md 附注
- 协作契约（Q31-Q33）→ USER/core.md 顶部

**规则：**
- 每次只出一题，等用户回答完再出下一题
- 每题附带简短的方向说明
- 不要一次列出多题
- 每答一题立即写入对应文件
- Q29-Q30 保留辅助参考，不强制回答

### A5：编译 GL1 + 生成报告
1. 读取 USER/core.md → 编译初始规则 → 写入 AGENTS/GL1-rules.md
2. 按 `{skill_dir}/assets/report-template.md` 生成《Agent-Memory 洞察报告》
   - 输出到：`$MEMORY_DATA/agent-memory-insight-report.md`

### A6：写入配置文件
创建/更新 `{skill_dir}/config.json`：
```json
{
  "version": "6.0.0",
  "memory_data_path": "$MEMORY_DATA",
  "activated": true,
  "last_used": "当前 ISO 时间"
}
```

### A7：完成
输出安装摘要：
- ✅ 配置已保存
- ✅ 目录结构已创建
- ✅ 各层数据已填充
- ✅ 报告已生成

末尾标记：`[🧠 Agent-Memory: 安装完成]`

---

## 工作流 B：健康检查

**触发：** 用户说"检查记忆" / "记忆状态"

### B1：扫描 $MEMORY_DATA 结构
检查：
- USER/core.md → 有内容/空/缺失
- USER/cognitive.md → 有内容/空/缺失
- USER/behavior.md → 有内容/空/缺失
- AGENTS/GL1-rules.md → 有内容/空/缺失
- AGENTS/GL2-patterns.md → 有内容/空/缺失
- AGENTS/project-index.md → 有内容/空/缺失
- questionnaire.md → 存在/缺失

### B2：检查配置文件
- config.json → 存在/格式正确/路径有效

### B3：输出报告
- 🟢 全部就绪 → 静默完成
- 🟡 部分缺失 → 列出缺失项，询问是否修复
- 🔴 严重缺失 → 提示重新安装

末尾标记：`[🧠 Agent-Memory: 健康检查]`

---

## 工作流 C：升级流程

**触发：** 用户说"升级记忆系统"

**原则：** 只替换系统文件，不动用户数据。

### C1：版本检测 + 自动更新
（保留原 skills CLI 更新逻辑，如果可用则使用；否则提示手动更新）

### C2：更新 assets 资源文件
1. 更新 `{skill_dir}/assets/AGENTS.md`
2. 更新 `{skill_dir}/assets/questionnaire.md`
3. 更新 `{skill_dir}/assets/report-template.md`
（注：实际通过技能更新机制完成）

### C3：更新题库（可选）
1. 比较 `$MEMORY_DATA/questionnaire.md` 与新版 `{skill_dir}/assets/questionnaire.md`
2. 有新增/修改题目 → 询问是否补答
3. 无变化 → 跳过

### C4：更新 config.json
更新版本号为 6.0.0，更新 last_used

### C5：健康检查 + 输出摘要
运行工作流 B（健康检查），输出升级摘要

**不动的内容**（不更新，不替换）：
- USER/core.md
- USER/cognitive.md
- USER/behavior.md
- AGENTS/GL1-rules.md
- AGENTS/GL2-patterns.md
- AGENTS/project-index.md

末尾标记：`[🧠 Agent-Memory: 升级完成]`

---

## 工作流 D：早晨规划

**触发：** "早上好" / "开始规划" / "今天做什么"

1. 获取系统时间
2. 读 `$MEMORY_DATA/USER/behavior.md`（L3 行为规律 — 高效时段/精力模式）
3. 读 `$WORKSPACE/memory/MEMORY.md`（L4 当前目标/卡点）
4. 读 `$MEMORY_DATA/AGENTS/project-index.md`（项目总览）
5. 读昨日日记（`$MEMORY_DATA/USER/diary/YYYY/MM/YYYY-MM-DD.md`）结转未完成
6. 基于以上信息引导制定今日 P1/P2 目标（含 🍅 预估）
7. 创建今日日记文件（仅写 YAML frontmatter + SSOT 任务骨架，道痕部分晚间补）
8. 末尾追加标记：`[🧠 Agent-Memory: 早晨规划]`

---

## 工作流 E：晚间复盘（核心）

**触发：** "今日复盘" / "晚间总结" / "写日记"

### E1：SSOT 数据补完
补全日志中以下数据（引导用户提供）：
- 入睡/起床时间
- 睡眠质量
- 总番茄数
- 能量状态
- 情绪评分（1-10）

### E2：道痕引导
逐层提问，**每次只问一层**，用户回答后再进行下一层。AI 记录用户原文到对应层。

**Q1：事实**
> 今天最让你起波澜的一件事是什么？只讲发生了什么，不评价不抒情。

**Q2：第一反应**
> 当时你的第一反应是什么？不是正确答案，是最直接的感觉。

**Q3：贪婪**
> 顺着那股劲，你其实想得到什么？不要用大词，写具体的。

**Q4：恐惧**
> 你其实在害怕什么？写最直接的那个怕。

**Q5：自洽**
> 你给了自己什么理由来消化这件事？你是怎么说服自己"这样也挺好"的？

**Q6：主石头**
> 今天捞出来的主石头是哪块？一句话：贪婪还是恐惧？具体是什么？

**Q7：人选练习**
> 如果明天再遇到同样的事，你准备怎么选？

### E3：石头追踪（L3 管线入口）
完成道痕后，自动执行：
1. 读取 `$MEMORY_DATA/USER/behavior.md` 中的石头列表
2. 对比今日主石头与历史石头
   - 新石头 → 记入今日日记 stones 字段
   - 同一本质出现 3+ 次 → 更新 `behavior.md`
3. 输出一句反馈

### E4：写入日记
写入 `$MEMORY_DATA/USER/diary/YYYY/MM/YYYY-MM-DD.md`，按日记模板输出。

### E5：L4 & 项目总览同步
- 如果今天有工作产出变化 → 更新 `$WORKSPACE/memory/MEMORY.md`
- 如果项目状态变化 → 更新 `$MEMORY_DATA/AGENTS/project-index.md`

### E6：明日预告
- 如果今天是周日 → "今天是周日，要不要顺便写周报？"

末尾追加标记：`[🧠 Agent-Memory: 晚间复盘]`

---

## 工作流 F：周报整理

**触发：** "写周报" / "周复盘"

1. 确定本周覆盖的日期范围
2. 如果跨月，读取两个月份目录的日记
3. 提取 SSOT 汇总：完成事项、时间分配、能量状态
4. 提取**重复石头列表**（跨天出现的同一本质主石头）
5. 对比上周计划与实际完成
6. 输出周报摘要给用户确认
7. 用户确认后写入周记（`$MEMORY_DATA/USER/diary/YYYY/MM/YYYY-Www.md`，放在天数较多的月份目录）
8. 提示："这周'[石头名]'出现了 N 次，是否确认写入 L3 behavior.md？"
9. 末尾追加标记：`[🧠 Agent-Memory: 周报整理]`

---

## 工作流 G：月度校准

**触发：** "月度校准"

**输入：** 本月所有日记 + 周记 + 本月工作区日志

### G1：日记 → L3 提炼
从本月日记、周记中提取行为规律：
- 扫描出现 3+ 次以上的行为模式
- 输出 L3 候选列表（含置信度和证据来源）
- 写入：`$MEMORY_DATA/USER/behavior.md`（行为段）

### G2：L3 → L2 归纳
L3 中置信度 ≥ 0.7 的模式升级为 L2 认知模式：
- 检查该模式是否已存在 L2
- 存在 → 合并证据，提升置信度
- 不存在 → 创建 L2 新条目
- 写入：`$MEMORY_DATA/USER/cognitive.md`（认知段）

### G3：L2 → L1 提案
L2 中置信度 ≥ 0.9 持续 3 个月的作为 L1 候选：
- 检查该模式是否稳定持续 3 个月以上
- 检查跨场景一致性
- 检查反例情况
- 输出 L1 候选提案，等用户确认后才写入 L1

### G4：L1 ↔ L3 一致性审计
对比 L1 说"你重视什么"和日记显示"你实际做了什么"：
- 逐条比对 L1 值与本月日记数据
- 计算差异
- 标记持续矛盾的条目
- 审计发现差异时，针对矛盾点生成 1-2 道追问，加入出题队列

### G5：更新 GL1 编译
L1/L2 更新后，重新编译 GL1 铁律：
- 检查本次 L1/L2 是否有实际变更
- 有变更 → 同步编译到 GL1（`$MEMORY_DATA/AGENTS/GL1-rules.md`）
- 无变更 → 跳过
- 编译规则：L1 底线 → GL1 铁律，L2 交互偏好 → GL1 沟通规则

### G6：成长箱晋升检查
参考架构定义的 GL2 晋升路径：
- 标记跨项目出现的规则
- 置信度 ≥ 0.7 且跨 2+ 项目 → 向用户提案晋升 GL1
- 置信度降到 0.3 以下 → 归档

### G7：输出汇总 + 写入月度日志
输出汇总报告，将本次校准结果追加到 `$MEMORY_DATA/USER/diary/YYYY/MM/monthly-log.md`

末尾标记：`[🧠 Agent-Memory: 月度校准]`

---

## 工作流 H：进度记账 / Session 日志

**触发：** "开始专注" / "完成" / "记账" / 对话结束自动

1. 用户报告进度 → 更新日记 SSOT 的"实际"列（番茄/状态）
2. 写工作区日志（追加到 `$WORKSPACE/memory/YYYY-MM-DD.md`，使用 Session 日志模板）
3. 检查是否需要更新 L4：
   - 状态有变化 → 更新 `$WORKSPACE/memory/MEMORY.md`
   - 无变化 → 跳过
4. 检查是否需要更新项目总览：
   - 项目进展有变化 → 更新 `$MEMORY_DATA/AGENTS/project-index.md`
   - 无变化 → 跳过
5. 简短确认（一句话），不打断心流
6. 末尾追加标记：`[🧠 Agent-Memory: 进度记账]`

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
