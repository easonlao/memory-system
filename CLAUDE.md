# OpenWolf

@.wolf/OPENWOLF.md

This project uses OpenWolf for context management. Read and follow .wolf/OPENWOLF.md every session. Check .wolf/cerebrum.md before generating code. Check .wolf/anatomy.md before reading files.


# CLAUDE.md

This file provides guidance when working with this repository (the `$MEMORY_ROOT` design directory).

## 仓库定位

Agent-Memory 的**设计目录**。存放框架定义文档和分发技能源。
运行时数据（`$MEMORY_DATA`）不在此仓库，由用户安装时指定。

## 架构概览

```
$MEMORY_DATA（运行时，用户安装时创建）
├── USER/         ← 用户画像（L1 价值观 + L2 认知 + L3 行为）
├── AGENTS/       ← AI 侧规则（GL1 铁律 + GL2 经验教训 + 项目总览）
└── 07-问卷.md    ← 题库存档

{workspace}/.memory/（工作区级）
├── MEMORY.md     ← L4 工作区状态快照
├── YYYY-MM-DD.md ← 工作区日志
└── .rules/       ← GL2b 项目规则
```

### 数据流向

```
用户日记/对话 → 月度校准提炼 → USER/L2-L3 → 持续稳定 → USER/L1
                                                    ↓
                                             编译 → AGENTS/GL1
对话观察/错误 → GL2c(临时) → 重复出现 → AGENTS/GL2 → 晋升 → AGENTS/GL1
```

## 核心文件

| 文件 | 用途 |
|------|------|
| `Agent-Memory/AGENTS.md` | **AI 入口** — 启动时加载，安装时写入平台 |
| `Agent-Memory/07-问卷.md` | 题库（带触发条件，系统动态出题） |
| `Agent-Memory/09-报告模板.md` | 洞察报告生成模板 |
| `Agent-Memory/01-架构定义.md` | 架构定义、目录结构 |
| `Agent-Memory/03-置信度体系.md` | 置信度规则 0.1-1.0 |
| `SKILL.md` | **唯一分发技能** — 安装入口 |

## 分发 vs 开发

### 分发文件（用户需要的全部）

```
      ← 唯一的安装入口
├── SKILL.md                  ← 安装工作流
├── metadata.json             ← 版本信息
└── references/               ← 子技能 + 模板 + 问卷
```

### 开发文件（我们维护的源）

```
Agent-Memory/                 ← 框架文档源（手动同步到 references/）
```

## 维护要点

- **升级不伤数据**：只替换技能目录，`$MEMORY_DATA` 不动
- **路径变量**：文档中 `$MEMORY_ROOT` = 本仓库路径，`$MEMORY_DATA` = 用户运行时数据
- **修改前**先确认需改哪些文件（框架源 + references/ 同步）
- **历史版本**在 `archived/` 目录下

## 开发工作流

### 修改框架文档

```
Agent-Memory/ 源文件 ← 编辑
    ↓ 手动同步
references/ ← 分发副本
```

同步映射（文件名可能不同）：

| 源文件 | 分发副本 |
|--------|---------|
| `Agent-Memory/AGENTS.md` | `references/AGENTS.md` |
| `Agent-Memory/07-问卷.md` | `references/questionnaire.md` |
| `Agent-Memory/09-报告模板.md` | `references/report-template.md` |
| `Agent-Memory/01~06.md` | 不分发（框架内部文档） |

### 版本发布

1. 更新 `metadata.json` 中 `version` 字段
2. 提交并打 tag：`git tag v<version>`
3. 推送到 remote：`git push && git push --tags`

### 常用命令

```bash
# 同步单个文件到分发目录
cp Agent-Memory/AGENTS.md references/

# 查看当前版本
cat metadata.json | grep version

# 存档旧版本
mv archived/v<旧版本>/ .

# 对比源文件和分发副本差异
diff Agent-Memory/07-问卷.md references/questionnaire.md
```

## 关联路径

- 本仓库 = `$MEMORY_ROOT`（设计目录）
- 运行时数据 = `$MEMORY_DATA`（用户指定，安装时创建）
- 工作区记忆 = `{workspace}/.memory/`（按项目隔离）

## Git 提交规范

参考 `Git 提交规范协议.md`，核心规则：

```
[<Type>]: <Subject>
```

| 类型 | 用途 |
|------|------|
| `feat` | 新增功能、新笔记页面、新逻辑 |
| `fix` | 修复代码 Bug、修正笔记错误 |
| `docs` | 纯文档润色、格式调整 |
| `refactor` | 代码重构、笔记结构重组 |
| `temp` | 临时存档（多设备同步前的中间状态） |

- **标题**：中文，祈使句，50 字内，末尾无标点
- **正文**：逻辑变更或多文件联动时**强制写 Body**，回答 Why 而非 What
- **多设备同步**场景自动标注 `[Sync]`
- commit 前先简述 diff 确认
