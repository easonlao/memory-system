# Agent-Memory v5.0

Let AI remember who you are. One install, always available, your data stays with you.

## Install

```bash
# Clone or download this repo, then:
npx skills add ./skills/memory-installer
# Or copy skills/memory-installer/ to your agent's skills directory
```

Then tell your AI: **"install memory system"**

The installer handles everything: platform entry config → sub-skill install → data directory setup → questionnaire.

## Features

- **One skill to rule them all** — memory-installer bundles everything
- **Your data, your control** — `$MEMORY_DATA` is the only backup you need
- **Cross-platform** — Claude Code, Cursor, Gemini CLI, GitHub Copilot, and more
- **Auto-maintained** — AI handles workspace logs, behavior extraction, collaboration patterns
- **Upgrade-safe** — Replace the skill directory, say "upgrade memory system", user data untouched

## Data Layout

Created during installation, no manual setup needed:

```
$MEMORY_DATA/
├── USER/                     ← Your profile (L1-L3)
│   ├── L1-core.md
│   └── L2-L3-rules.md
└── AGENTS/                   ← AI-side data
    ├── GL1-rules.md
    ├── GL2-patterns.md
    └── project-index.md
```
