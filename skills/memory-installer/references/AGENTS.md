# Agent-Memory — AI Template

Auto-written to platform entry file during installation.

---

## Startup Flow

```
0. Check $MEMORY_DATA
   ├── Known → skip
   ├── Known but no entry file → call memory-installer skill as entry
   └── Unknown → call memory-installer skill for setup

1. pwd → $WORKSPACE

2. Check $WORKSPACE/.memory/MEMORY.md
   ├── Exists → read (current goals/blocks)
   └── Missing → create directory

3. Check $WORKSPACE/.memory/ for recent YYYY-MM-DD.md
   ├── Found today/yesterday → read (session continuity)
   └── None → skip

4. Read GL1 ($MEMORY_DATA/AGENTS/GL1-rules.md)
5. Read GL2 ($MEMORY_DATA/AGENTS/GL2-patterns.md)
```

## System Rules

| Condition | Definition | Action |
|-----------|-----------|--------|
| Repeated errors | Same issue corrected ≥ 2x / consecutive failures / repeated fix requests | Log to GL2c (error + count) |
| L4 state change | New project / goal completed / blocker changed / last update long ago | Ask: "Workspace state changed, update workspace memory?" |
