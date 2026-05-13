# Agent-Memory

一体化个人 AI 记忆系统。帮助 AI 理解用户、建立长期记忆。

## 仓库定位

本仓库是 Agent-Memory 的设计目录。运行时数据（`$MEMORY_DATA`）由用户安装时指定，不在此仓库。

## 目录结构

```
memory-system/               ← 本仓库根目录
├── AGENTS.md               ← AI 入口（本文档）
├── README.md               ← 项目文档
├── LICENSE                 ← MIT 许可
├── metadata.json           ← 项目元数据
├── .gitignore              ← Git 配置
├── skills/
│   └── memory-system/      ← 唯一发布目录（用户复制这个）
│       ├── SKILL.md        ← 技能入口
│       ├── AGENTS.md       ← AI 模板
│       ├── metadata.json   ← 技能版本信息
│       ├── README.md       ← 用户安装说明
│       └── assets/         ← 静态资源
│           ├── AGENTS.md
│           ├── questionnaire.md
│           └── report-template.md
├── archived/               ← 历史版本归档（已 gitignore）
├── design/                 ← 按模块组织的设计文档
│   ├── 01-architecture.md
│   ├── 02-confidence-system.md
│   ├── 03-startup-flow.md
│   ├── 04-installation.md
│   ├── 05-system-maintenance.md
│   ├── 06-morning-planning.md
│   ├── 07-evening-review.md
│   ├── 08-weekly-report.md
│   ├── 09-monthly-calibration.md
│   └── 10-progress-logging.md
├── .claude/                ← 开发环境配置（已 gitignore）
├── .wolf/                  ← OpenWolf 上下文管理（已 gitignore）
├── .memory/                ← 本工作区记忆（已 gitignore）
└── docs/                   ← 开发文档（已 gitignore）
```

## 核心文件

| 文件 | 用途 |
|------|------|
| `skills/memory-system/SKILL.md` | 技能入口，包含所有工作流 |
| `skills/memory-system/AGENTS.md` | AI 模板，用户运行时加载 |
| `skills/memory-system/assets/questionnaire.md` | 用户画像题库 |
| `skills/memory-system/assets/report-template.md` | 洞察报告生成模板 |
| `design/*.md` | 按模块组织的设计文档（架构/置信度/启动/安装/维护/规划/复盘/周报/校准/记账） |

## 数据流向（运行时）

```
用户日记/对话 → 月度校准提炼 → USER/L2-L3 → 持续稳定 → USER/L1
                                                    ↓
                                             编译 → AGENTS/GL1
对话观察/错误 → GL2c(临时) → 重复出现 → AGENTS/GL2 → 晋升 → AGENTS/GL1
```

## 开发工作流

### 修改技能文件

直接编辑 `skills/memory-system/` 下的文件即可：
- `SKILL.md` — 修改工作流逻辑
- `assets/AGENTS.md` — 修改 AI 模板
- `assets/questionnaire.md` — 修改题库
- `assets/report-template.md` — 修改报告模板

### 版本发布

1. 更新 `skills/memory-system/metadata.json` 中 `version` 字段
2. 提交并打 tag：`git tag v<version>`
3. 推送到 remote：`git push && git push --tags`

### 存档旧版本

```bash
mkdir archived/v<旧版本>
cp -r skills/memory-system archived/v<旧版本>/
```

### 升级原则

只替换技能目录，`$MEMORY_DATA` 不动。

## Git 提交规范

```
[<Type>]: <Subject>
```

| 类型 | 用途 |
|------|------|
| `feat` | 新增功能、新逻辑 |
| `fix` | 修复 Bug、修正错误 |
| `docs` | 纯文档润色、格式调整 |
| `refactor` | 代码重构、结构重组 |
| `temp` | 临时存档（多设备同步前的中间状态） |

- **标题**：中文，祈使句，50 字内，末尾无标点
- **正文**：逻辑变更或多文件联动时**强制写 Body**，回答 Why 而非 What
- 多设备同步场景自动标注 `[Sync]`
- commit 前先简述 diff 确认