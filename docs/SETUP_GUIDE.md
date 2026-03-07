# Setup Guide

Complete guide to setting up your OpenClaw multi-agent team.

## Prerequisites

- OpenClaw installed and running
- GitHub account (for forking this template)
- Basic familiarity with markdown

## Step 1: Fork the Template

1. Go to the template repository on GitHub
2. Click "Use this template" → "Create a new repository"
3. Name your repository
4. Choose public or private
5. Click "Create repository"

## Step 2: Clone Your Repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
```

## Step 3: Customize the Orchestrator

Edit `SOUL.md` to define your orchestrator's personality:

```markdown
# SOUL.md - Orchestrator Persona

**Name:** [Your orchestrator's name]
**Creature:** [What they are]
**Emoji:** [Their signature emoji]
**Role:** Team lead, decision maker

## Personality
[Define how they communicate and lead]

## Team Dynamics
[How they interact with agents]
```

## Step 4: Customize Agents

For each agent in `agents/`:

1. Edit `SOUL.md` - Define personality
2. Edit `USAGE.md` - Document capabilities
3. Edit `CONFIG.md` - Set preferences

### Agent Customization Checklist

- [ ] 🦉 Researcher (`agents/mat-cu/`)
- [ ] 🐱 Secretary (`agents/tieu-mi/`)
- [ ] 🐭 Engineer (`agents/ti-can/`)
- [ ] 🦋 Designer (`agents/tieu-hoa/`)

## Step 5: Update Team Documentation

Edit these files to match your setup:

### AGENTS.md
Update the team roster with your agents' names and roles.

### ORCHESTRATION_WORKFLOW.md
Customize the workflow to match your team's processes.

### USER.md
Fill in information about yourself (the user).

## Step 6: Configure Tools

Edit `TOOLS.md` to add your environment-specific notes:

```markdown
### SSH
- my-server → [IP/hostname]

### API Keys
- Service: [How to access]

### Preferences
- Default voice: [For TTS]
```

## Step 7: Set Up Identity

Edit `IDENTITY.md` for each agent:

```markdown
- **Name:** [Agent's chosen name]
- **Creature:** [What they are]
- **Vibe:** [How they come across]
- **Emoji:** [Their signature]
```

## Step 8: Configure Heartbeat

Edit `HEARTBEAT.md` to define periodic tasks:

```markdown
## My Custom Checks
- [ ] Check emails
- [ ] Review calendar
- [ ] Monitor [specific thing]
```

## Step 9: Test Your Setup

1. Start a new session with your orchestrator
2. Try delegating a simple task to each agent
3. Verify the workflow feels natural
4. Adjust personalities as needed

## Step 10: Commit Your Changes

```bash
git add .
git commit -m "Customize multi-agent team setup"
git push origin main
```

## Next Steps

- Read [CUSTOMIZATION.md](CUSTOMIZATION.md) for advanced options
- See [EXAMPLES.md](EXAMPLES.md) for workflow examples
- Start using your team for real tasks!

## Troubleshooting

### Agents not responding as expected
- Check their `SOUL.md` files
- Verify prompts are clear
- Adjust personalities if needed

### Workflow feels clunky
- Simplify the orchestration
- Reduce handoff steps
- Automate where possible

### Memory not persisting
- Ensure `memory/` folder exists
- Check file permissions
- Verify `.gitignore` excludes sensitive files

## Support

- OpenClaw documentation: [Link]
- Template issues: [Your repo issues]
- Community: [Discord/Forum link]