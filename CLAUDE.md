# OpenWolf

@.wolf/OPENWOLF.md

This project uses OpenWolf for context management. Read and follow .wolf/OPENWOLF.md every session. Check .wolf/cerebrum.md before generating code. Check .wolf/anatomy.md before reading files.


# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

## 仓库定位

这是五层记忆系统的**公共文件夹**（`$MEMORY_ROOT`），存放所有跨平台共享的记忆数据和文档源文件。文件由 SynologyDrive 在多设备间同步。

## 核心文档

| 文件 | 用途 |
|------|------|
| `五层记忆系统/README.md` | **系统入口** — 路由表、系统概览、文件索引（AI 首读） |
| `五层记忆系统/01-架构定义.md` | L1-L4 定义、数据流向、目录结构 |
| `五层记忆系统/02-入口与加载机制.md` | 加载顺序、路由机制 |
| `五层记忆系统/03-置信度体系.md` | 置信度规则 |
| `五层记忆系统/04-通用规则.md` | G1-G11 + I1-I7 |
| `五层记忆系统/05-成长箱机制.md` | GL1/GL2 定义、晋升流程 |
| `五层记忆系统/06-管理流程.md` | 成长箱自动沉淀流程 |
| `五层记忆系统/07-问卷.md` | Q1-Q33 |
| `五层记忆系统/09-报告模板.md` | 洞察报告模板 |
| `技能配置/` | 记忆助理/月度校准/工作区记忆维护/唤醒/读书助手 Skill |

## 编辑规范

- **路径变量**：文档中使用 `$MEMORY_ROOT` 占位公共文件夹路径，本仓库即 `E:\SynologyDrive\Memory\源文件`
- **修改文件前**先输出修改清单，等用户确认后再写入
- **更新日志**：任何重要修改都应在 `更新日志.md` 中追加记录

## 关联路径

- 本仓库 = `$MEMORY_ROOT`（公共文件夹根目录）
- 项目级工作记忆存放于 `{工作区}/.memory/`（按项目隔离，不在本仓库）