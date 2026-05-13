# Agent-Memory (v6)

一体化个人 AI 记忆系统。单文件夹复制即用，无需配置平台入口文件。

## 安装

```bash
npx skills add easonlao/memory-system
```

或直接复制 `skills/memory-system/` 目录到你的 AI 平台的 skills 目录。

然后对 AI 说 **"使用记忆系统"**。

安装向导会自动完成：配置 → 创建数据目录 → 引导问卷填充。

## 功能

- 日记与早晚规划
- 周报与月度校准
- 四层记忆体系（L1-L4）
- AI 行为规则自动进化

## 目录结构

```
memory-system/
├── AGENTS.md              ← 项目入口（AI 读取了解项目）
├── README.md              ← 本文档
├── LICENSE                ← MIT 许可
├── skills/
│   └── memory-system/     ← 技能（用户复制这个）
│       ├── SKILL.md       ← 技能入口
│       ├── AGENTS.md      ← AI 模板
│       ├── metadata.json
│       └── assets/        ← 静态资源
├── design/                ← 设计文档（本地开发）
└── archived/              ← 历史版本归档
```

## 信号词

- "使用记忆系统" — 安装/激活
- "早上好" / "开始规划" — 早晨规划
- "今日复盘" / "写日记" — 晚间复盘
- "写周报" / "周复盘" — 周报整理
- "月度校准" — 月度校准
- "检查记忆" — 健康检查
- "升级记忆系统" — 升级

## 特点

- **一个技能搞定全系统** — memory-system 自带所有依赖
- **你掌控数据** — `$MEMORY_DATA` 目录是唯一需要备份的，迁移时复制即可
- **跨平台** — Claude Code、Cursor、Gemini CLI、GitHub Copilot 等
- **自动维护** — AI 在后台管理工作区日志、行为提炼
- **升级不影响数据** — 替换技能目录后说"升级记忆系统"即可

## 从 v5.x 升级

1. 备份你的 `$MEMORY_DATA` 目录
2. 用新版本替换整个 `memory-system` 文件夹
3. 首次运行时会自动检测已有数据并创建配置