---
name: memory-installer
description: One-click memory system installer. Guides first-time setup: configures platform entry, installs sub-skills (memory-assistant, monthly-calibration, workspace-memory), creates data directories, drives questionnaire. Also handles health checks and system upgrades. Use when user mentions "memory", "install memory", "memory system", or when $MEMORY_DATA is not set.
---

# 🧠 Agent-Memory Installer

> The only skill you need to install. After setup, all sub-skills (memory-assistant, monthly-calibration, workspace-memory) are automatically ready.
> All dependency files located at `{skill_dir}/references/`.

---

## Workflow A: First-time Installation

> Triggered when `$MEMORY_DATA` is not set. Guides the user through full setup.

### Step 1: Configure Platform Entry

```
1. Ask user which AI platform they use:
   ├── Claude Code   → entry: .claude/CLAUDE.md
   ├── Cursor        → entry: .cursorrules
   ├── Gemini CLI    → entry: GEMINI.md
   ├── GitHub Copilot→ entry: .github/copilot-instructions.md
   └── Other         → ask user for entry file path

2. Read {skill_dir}/references/AGENTS.md
   Append to platform entry file (create if not exists)

3. ⚠️ If entry file cannot be found/created:
   Output AGENTS.md content for manual copy
   This skill will act as entry point each session
```

### Step 2: Install Sub-skills

```
1. Determine platform skills directory
   ├── Claude Code → .claude/skills/
   └── Other → ask user for skills directory

2. Copy sub-skills:
   ├── memory-assistant   → {skills_dir}/memory-assistant/SKILL.md
   ├── monthly-calibration → {skills_dir}/monthly-calibration/SKILL.md
   ├── workspace-memory   → {skills_dir}/workspace-memory/SKILL.md
   └── reading-assistant  → ask user if wanted
```

### Step 3: Set Runtime Data Directory

```
1. Ask user for $MEMORY_DATA path
   Recommend: ~/.memory-data/ or cloud sync folder

2. mkdir -p $MEMORY_DATA/{USER,AGENTS}

3. Copy {skill_dir}/references/questionnaire.md to $MEMORY_DATA/
   Inform: this is the only directory to back up

4. Write $MEMORY_DATA to top of platform entry file:
   $MEMORY_DATA = {user_path}
```

### Step 4: Questionnaire

```
Guide through $MEMORY_DATA/questionnaire.md section by section:

Part 1 Core (Q1-Q7)       → write to USER/L1-core.md
Part 2 Cognition (Q8-Q17)  → write to USER/L2-L3-rules.md (L2 section)
Part 3 Behavior (Q18-Q23)  → write to USER/L2-L3-rules.md (L3 section)
Part 4 Context (Q24-Q28)   → appendix notes
Contract (Q31-Q33)         → top of L1-core.md

Write after each answer. Q29-Q30 auxiliary only.
```

### Step 5: Compile GL1 + Generate Report

```
1. Read USER/L1-core.md → compile initial rules → write AGENTS/GL1-rules.md

2. Using {skill_dir}/references/report-template.md
   Generate "Agent-Memory Insight Report"
   Output to $MEMORY_DATA/agent-memory-insight-report.md
```

### Step 6: Done

```
Output summary:
- Platform entry configured
- X sub-skills installed
- $MEMORY_DATA set
- User data populated
- Report generated
```

---

## Workflow B: Health Check

> Triggered when user says "check memory", "memory status", or on startup.

```
1. Scan $MEMORY_DATA structure
├── USER/L1-core.md          → has content/empty/missing
├── USER/L2-L3-rules.md      → has content/empty/missing
├── AGENTS/GL1-rules.md      → has content/empty/missing
├── AGENTS/GL2-patterns.md   → has content/empty/missing
├── AGENTS/project-index.md  → has content/empty/missing
└── questionnaire.md         → exists/missing

2. Scan skills directory
├── memory-assistant     → installed/missing
├── monthly-calibration  → installed/missing
└── workspace-memory     → installed/missing

3. Report
🟢 All good → silent
🟡 Partial  → list missing items, ask to fix
🔴 Critical → prompt reinstall
```

---

## Workflow C: Upgrade

> Triggered when user says "upgrade memory system".
> **Principle: replace system files only, never touch user data.**

```
1. Verify $MEMORY_DATA is known

2. Update entry file
   ├── Re-read {skill_dir}/references/AGENTS.md
   ├── Compare with existing entry
   └── Changed → prompt user to manually replace entry content

3. Update sub-skills
   ├── Detect installed skills
   ├── Overwrite memory-assistant (if installed)
   ├── Overwrite monthly-calibration (if installed)
   ├── Overwrite workspace-memory (if installed)
   └── reading-assistant → ask if newly wanted

4. Update questionnaire
   ├── Compare $MEMORY_DATA/questionnaire.md with new version
   └── Questions added/changed → ask user to complete

5. Run health check
   └── Output upgrade summary
```

**Never touched during upgrade:**
- USER/L1-core.md
- USER/L2-L3-rules.md
- AGENTS/GL1-rules.md
- AGENTS/GL2-patterns.md
- AGENTS/project-index.md

---

## Marker

Append at end of reply: `[🧠 Agent-Memory: {install/check/upgrade}]`
