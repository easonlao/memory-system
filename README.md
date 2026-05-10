# Agent-Memory v5.0

让 AI 理解你的记忆框架。一次安装，持久可用，数据你掌控。

## 安装

```bash
npx skills add easonlao/memory-system/tree/main/skills/memory-installer
```

或直接将 `skills/memory-installer/` 复制到你的 AI 平台的 skills 目录。
```

然后对 AI 说 **"install memory system"**。

安装向导会自动完成：配置入口 → 安装子技能 → 创建数据目录 → 引导问卷填充。

## 特点

- **一个技能搞定全系统** — memory-installer 自带所有依赖
- **你掌控数据** — `$MEMORY_DATA` 目录是唯一需要备份的，迁移时复制即可
- **跨平台** — Claude Code、Cursor、Gemini CLI、GitHub Copilot 等
- **自动维护** — AI 在后台管理工作区日志、行为提炼、合作规律
- **升级不影响数据** — 替换技能目录后说"upgrade memory system"即可

## 数据目录结构

安装后自动生成，你不需要手动创建：

```
$MEMORY_DATA/
├── USER/                     ← 你的画像（L1-L3）
│   ├── core.md
│   ├── cognitive.md
│   ├── behavior.md
│   ├── diary/
└── AGENTS/                   ← AI 侧数据
    ├── GL1-rules.md
    ├── GL2-patterns.md
    └── project-index.md
```
