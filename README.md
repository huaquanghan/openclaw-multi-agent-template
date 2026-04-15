# Quả Quả + Teams Template

> 🍑 A practical OpenClaw template for building one assistant first, then growing into sub-agents and specialist teams when needed.

## Overview

This repository is a reusable base for creating more assistants in the **Quả Quả + Teams** style.

The core idea is simple:
- **Quả Quả** is the main identity and user-facing orchestrator
- **teams** are modular capability layers that can stay lightweight at first
- delegation can later be implemented with **OpenClaw sub-agents**, persistent specialists, or channel-specific routing

This means the template works in three modes:
1. **Quả Quả only**
2. **Quả Quả + sub-agents**
3. **Quả Quả + persistent specialist agents**

## What this template is for

Use this repo when you want:
- one warm, coherent assistant identity at the center
- a clean path from single-agent to team-based orchestration
- practical workflow docs, handoff rules, and memory habits
- optional long-term knowledge layering with systems like GBrain

## Features

- 🍑 **Identity-first design** - the assistant feels like a real consistent helper, not just a router
- 🧩 **Modular teams** - specialist roles can stay as docs or become real sub-agents later
- 🔄 **Quả Quả-led orchestration** - bounded delegation, review, synthesis, final delivery
- 🧠 **Layered memory model** - workspace, memory files, and optional durable knowledge layer
- 🛠️ **Replication-friendly** - fork this base to spin up another Quả Quả cleanly

## Quick Start

### 1. Use this template

Fork it or click GitHub's template button.

### 2. Clone your copy

```bash
git clone https://github.com/YOUR_USERNAME/openclaw-multi-agent-template.git
cd openclaw-multi-agent-template
```

### 3. Customize the identity layer

Start with the root files:
- `SOUL.md` - who your Quả Quả is
- `IDENTITY.md` - name, emoji, vibe
- `USER.md` - who the assistant is helping
- `AGENTS.md` - workspace law and team map

### 4. Customize the teams layer

Edit `agents/` only as much as you need:
- `SOUL.md` - specialist persona
- `USAGE.md` - when to use that specialist
- `CONFIG.md` - technical/runtime notes
- `IDENTITY.md` - quick roster metadata

### 5. Pick an implementation mode

- **Minimal:** Quả Quả does most work directly
- **Sub-agent mode:** Quả Quả delegates bounded tasks to OpenClaw sub-agents
- **Persistent mode:** specialists get longer-lived contexts or separate channels

### 6. Start with the orchestration workflow

Read [`ORCHESTRATION_WORKFLOW.md`](ORCHESTRATION_WORKFLOW.md) and use it as the default routing contract.

## Team Structure

| Layer | Role | Purpose |
|-------|------|---------|
| **Quả Quả** | Core orchestrator | Owns the relationship, decides, delegates, synthesizes |
| **Mắt Cú** | Research team | Research, fact-checking, synthesis |
| **Tiểu Mỉ** | Coordination team | Notes, reminders, schedules, checklists |
| **Tí Cận** | Build team | Coding, debugging, DevOps, implementation |
| **Tiểu Hoa** | Design team | Visuals, UI/UX, presentation |

## Knowledge Model

This template supports a layered model:
- **workspace files** for active execution and local operating rules
- **memory files** for continuity and personal context
- **durable knowledge** such as GBrain when a separate long-term knowledge layer is useful

Durable knowledge is optional. The minimal template does not require it.

## Documentation

- [SETUP_GUIDE.md](docs/SETUP_GUIDE.md) - detailed setup instructions
- [CUSTOMIZATION.md](docs/CUSTOMIZATION.md) - how to adapt the template
- [EXAMPLES.md](docs/EXAMPLES.md) - workflow examples
- [ORCHESTRATION_WORKFLOW.md](ORCHESTRATION_WORKFLOW.md) - Quả Quả-led delegation flow
- [QUAQUA_TEAMS_TEMPLATE_SPEC.md](docs/QUAQUA_TEAMS_TEMPLATE_SPEC.md) - target framing for this template

## File Structure

```
.
├── README.md                    # Template overview
├── AGENTS.md                    # Workspace law + team map
├── SOUL.md                      # Quả Quả core persona
├── ORCHESTRATION_WORKFLOW.md    # Delegation and synthesis rules
├── USER.md                      # Human context template
├── TOOLS.md                     # Local tools/setup notes
├── IDENTITY.md                  # Quick identity metadata
├── HEARTBEAT.md                 # Periodic task template
├── .context/                    # Cached API/reference context
├── shared/                      # Shared workflow artifacts
├── assets/                      # Logos, avatars, visuals
├── agents/                      # Team capability packs
│   ├── mat-cu/                  # Research team
│   ├── tieu-mi/                 # Coordination team
│   ├── ti-can/                  # Build team
│   └── tieu-hoa/                # Design team
├── memory/                      # Daily notes storage
└── docs/                        # Setup, customization, replication docs
```

## License

MIT License - See [LICENSE](LICENSE) for details.

---

Built with 🍑 for OpenClaw-based assistants that need both personality and structure.
