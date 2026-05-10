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
├── AGENTS/       ← AI 侧规则（GL1 铁律 + GL2 模式候选 + 项目总览）
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
| `README.md` | **用户安装指南** — 用户看 |
| `Agent-Memory/AGENTS.md` | **AI 模板** — 安装时写入平台入口 |
| `Agent-Memory/07-问卷.md` | 33 题问卷，安装时引导填充 |
| `Agent-Memory/09-报告模板.md` | 洞察报告生成模板 |
| `Agent-Memory/01-架构定义.md` | 架构定义、目录结构 |
| `Agent-Memory/03-置信度体系.md` | 置信度规则 0.1-1.0 |
| `Agent-Memory/04-通用规则.md` | G1-G11 + I1-I7 |
| `Agent-Memory/05-成长箱机制.md` | GL1/GL2 晋升流程 |
| `Agent-Memory/06-管理流程.md` | 成长箱自动沉淀流程 |
| `skills/memory-installer/SKILL.md` | **唯一分发技能** — 安装入口 |

## 分发 vs 开发

### 分发文件（用户需要的全部）

```
skills/memory-installer/      ← 唯一的安装入口
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

## 关联路径

- 本仓库 = `$MEMORY_ROOT`（设计目录）
- 运行时数据 = `$MEMORY_DATA`（用户指定，安装时创建）
- 工作区记忆 = `{workspace}/.memory/`（按项目隔离）
