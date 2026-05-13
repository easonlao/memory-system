# 工作流 A：安装流程

触发：首次使用（无 config.json）/ "安装记忆系统" / "重新配置"

## A1：配置 $MEMORY_DATA 路径
1. 询问用户选择 $MEMORY_DATA 路径
   - 建议：~/.memory-data/ 或云盘同步目录
2. 验证路径有效性

## A2：创建目录结构
1. 创建：`$MEMORY_DATA/USER/`
2. 创建：`$MEMORY_DATA/AGENTS/`
3. 创建：`$MEMORY_DATA/USER/diary/`
4. 创建：`$MEMORY_DATA/.amber/` 记忆琥珀目录
   - `$MEMORY_DATA/.amber/USER/core/`
   - `$MEMORY_DATA/.amber/USER/cognitive/`
   - `$MEMORY_DATA/.amber/USER/behavior/`
   - `$MEMORY_DATA/.amber/AGENTS/GL1/`
   - `$MEMORY_DATA/.amber/AGENTS/GL2/`

## A3：复制题库
1. 复制 `{skill_dir}/assets/questionnaire.md` → `$MEMORY_DATA/questionnaire.md`
2. 告知用户：这是唯一需要备份的目录，迁移时完整复制即可

## A4：问卷填充
引导用户逐部分回答 `$MEMORY_DATA/questionnaire.md`：
- 第一部分 核心层（Q1-Q7）→ 写入 USER/core.md
- 第二部分 认知层（Q8-Q17）→ 写入 USER/cognitive.md（放入 `## 问卷` 段，不标记来源，永不衰减）
- 第三部分 行为层（Q18-Q23）→ 写入 USER/behavior.md（放入 `## 问卷` 段，不标记来源，永不衰减）
- 第四部分 情境层（Q24-Q28）→ USER/behavior.md 附注
- 协作契约（Q31-Q33）→ USER/core.md 顶部

规则：
- 每次只出一题，等用户回答完再出下一题
- 每题附带简短的方向说明
- 不要一次列出多题
- 每答一题立即写入对应文件
- Q29-Q30 保留辅助参考，不强制回答

## A5：编译 GL1 + 生成报告
1. 读取 USER/core.md → 编译初始规则 → 写入 AGENTS/GL1-rules.md
2. 按 `{skill_dir}/assets/report-template.md` 中的报告模板生成底层洞察报告
   - 输出到：`$MEMORY_DATA/底层洞察与协作契约报告-YYYY-MM-DD.md`

## A6：写入配置文件
创建/更新 `{skill_dir}/config.json`：
```json
{
  "version": "6.1.0",
  "memory_data_path": "$MEMORY_DATA",
  "activated": true,
  "last_used": "当前 ISO 时间"
}
```

## A7：完成
输出安装摘要：
- ✅ 配置已保存
- ✅ 目录结构已创建
- ✅ 各层数据已填充
- ✅ 报告已生成

末尾追加标记：`[🧠 Agent-Memory: 安装完成]` + `[🧠 路由: 系统]`

执行完毕后，按 SKILL.md 通用推荐规则推荐下一步。
