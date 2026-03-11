# OpenClaw Multi-Agent Template

> 🐯 A production-ready template for building multi-agent teams with OpenClaw

## Overview

This template provides a complete foundation for orchestrating multiple AI agents working together on complex tasks. Inspired by the "Cọp và Đàn Em" (Tiger and Cubs) team structure, it demonstrates how to effectively delegate, coordinate, and manage specialized agents.

## Features

- 🎯 **Clear Role Definitions** - Each agent has a specific persona and responsibilities
- 🔄 **Orchestration Workflow** - Battle-tested patterns for task delegation
- 📚 **Documentation** - Comprehensive guides for setup and customization
- 🧠 **Memory System** - Persistent context across sessions
- 🛠️ **Ready to Use** - Fork and start building immediately

## Quick Start

### 1. Fork this Repository

Click the "Use this template" button or fork directly on GitHub.

### 2. Clone Your Copy

```bash
git clone https://github.com/YOUR_USERNAME/openclaw-multi-agent-template.git
cd openclaw-multi-agent-template
```

### 3. Customize Your Team

Edit the agent configurations in `agents/`:
- `SOUL.md` - Define each agent's personality
- `USAGE.md` - Document how to use each agent
- `CONFIG.md` - Set technical parameters

### 4. Update Orchestrator

Edit `SOUL.md` at the root to define your orchestrator's persona.

### 5. Start Using

Follow the workflow in `ORCHESTRATION_WORKFLOW.md` to begin delegating tasks.

## Team Structure

| Agent | Role | Emoji | Description |
|-------|------|-------|-------------|
| **Cọp** | Orchestrator | 🐯 | Coordinates the team, makes decisions |
| **Mắt Cú** | Researcher | 🦉 | Gathers information, fact-checks |
| **Tiểu Mỉ** | Secretary | 🌸 | Manages tasks, schedules, reminders |
| **Tí Cận** | Software Engineer | 💻 | Codes, debugs, builds, DevOps |
| **Tiểu Hoa** | Designer | 🎨 | Creates visuals, UI/UX design |

## Documentation

- [SETUP_GUIDE.md](docs/SETUP_GUIDE.md) - Detailed setup instructions
- [CUSTOMIZATION.md](docs/CUSTOMIZATION.md) - How to customize for your needs
- [EXAMPLES.md](docs/EXAMPLES.md) - Real-world workflow examples
- [ORCHESTRATION_WORKFLOW.md](ORCHESTRATION_WORKFLOW.md) - Task delegation patterns

## File Structure

```
.
├── README.md                    # This file
├── AGENTS.md                    # Team overview and standards
├── SOUL.md                      # Orchestrator persona
├── ORCHESTRATION_WORKFLOW.md    # Workflow documentation
├── USER.md                      # User context template
├── TOOLS.md                     # Tools notes template
├── IDENTITY.md                  # Identity template
├── HEARTBEAT.md                 # Periodic tasks template
├── agents/                      # Agent configurations
│   ├── mat-cu/                  # Researcher agent
│   ├── tieu-mi/                 # Secretary agent
│   ├── ti-can/                  # Engineer agent
│   └── tieu-hoa/                # Designer agent
├── memory/                      # Daily notes storage
└── docs/                        # Additional documentation
```

## License

MIT License - See [LICENSE](LICENSE) for details.

## Contributing

This is a template repository. Feel free to:
- Fork and customize for your needs
- Submit issues for improvements
- Share your customizations

---

Built with 🐯 by the OpenClaw community