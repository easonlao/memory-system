# 五层记忆系统 v5.0 — 公共记忆库入口

`$MEMORY_ROOT` = `E:\SynologyDrive\Memory\源文件`

---

## 一、启动流程

```
1. pwd → $WORKSPACE

2. 检查 $WORKSPACE/.memory/MEMORY.md
   ├── 存在 → 读取（当前目标/卡点）
   └── 不存在 → 创建目录

3. 检查 $WORKSPACE/.memory/ 目录下最近的 YYYY-MM-DD.md
   ├── 有今日/昨日的文件 → 读取（脉络衔接）
   └── 没有 → 跳过

4. 读取 GL1（$MEMORY_ROOT/AGENTS/GL1-铁律.md）
5. 读取 GL2（$MEMORY_ROOT/AGENTS/GL2-模式候选.md）
```

---

## 二、系统规则（无对应 Skill）

| 条件 | 定义 | 执行 |
|------|------|------|
| 同类错误反复 | 同一问题被纠正 ≥ 2 次 / 连续报错 / 重复修改 | 记录到 GL2c（含错误描述 + 次数）|
| L4 状态明显变化 | 新项目 / 目标完成 / 卡点变化 / 距上次更新已久 | 主动询问是否更新工作区记忆 |
