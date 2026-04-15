# Setup Guide

Complete guide to setting up your **Quả Quả + Teams** OpenClaw template.

## What you are setting up

This template supports three modes:
1. **Quả Quả only**
2. **Quả Quả + sub-agents**
3. **Quả Quả + persistent specialists**

Start simple. You can add more orchestration later.

## Prerequisites

- OpenClaw installed and running
- GitHub account if you want to fork this template
- Basic familiarity with markdown

## Step 1: Fork the template

1. Go to the template repository on GitHub
2. Click "Use this template"
3. Create your repository
4. Choose public or private

## Step 2: Clone your repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
```

## Step 3: Customize the identity layer

Start with the root files:
- `SOUL.md` - define who Quả Quả is
- `IDENTITY.md` - name, emoji, vibe
- `USER.md` - who the assistant is helping
- `AGENTS.md` - workspace law and team map

Example shape for `SOUL.md`:

```markdown
# SOUL.md - Core Persona

**Name:** [assistant name]
**Creature:** [what they are]
**Emoji:** [signature emoji]
**Role:** User-facing orchestrator

## Personality
[How they communicate]

## Delegation Rules
[When they should do the work directly vs delegate]
```

## Step 4: Customize the teams layer

For each specialist in `agents/`:
1. Edit `SOUL.md`
2. Edit `USAGE.md`
3. Edit `CONFIG.md`
4. Edit `IDENTITY.md`

### Team checklist
- [ ] 🦉 Mắt Cú, research and synthesis
- [ ] 🐱 Tiểu Mỉ, coordination and notes
- [ ] 🐭 Tí Cận, build and technical work
- [ ] 🦋 Tiểu Hoa, design and visuals

## Step 5: Pick your runtime mode

### Mode 1: Quả Quả only
- keep everything lightweight
- use team docs as routing/thinking aids

### Mode 2: Quả Quả + sub-agents
- Quả Quả stays user-facing
- specialists run as bounded workers
- recommended default once delegation starts being useful

### Mode 3: Quả Quả + persistent specialists
- use only when repeated workload justifies more complexity

## Step 6: Update workflow docs

Review and adjust:
- `AGENTS.md`
- `ORCHESTRATION_WORKFLOW.md`
- `USER.md`
- `TOOLS.md`

Make sure the docs all agree on:
- who Quả Quả is
- when delegation happens
- how specialists hand work back

## Step 7: Configure tools and local notes

Use `TOOLS.md` for setup-specific notes:

```markdown
### SSH
- app-server -> [hostname]

### Services
- calendar source -> [how it is connected]

### Preferences
- preferred voice -> [value]
```

## Step 8: Configure heartbeat and memory

- `HEARTBEAT.md` for recurring checks
- `memory/YYYY-MM-DD.md` for daily continuity
- `MEMORY.md` for curated long-term context

## Step 9: Test the setup

### Minimal test
1. Start a session with Quả Quả
2. Ask for a small task
3. Verify the voice and behavior feel right

### Sub-agent test
1. Ask Quả Quả to split a task into research + build
2. Verify delegation stays bounded
3. Verify Quả Quả synthesizes before replying

## Step 10: Commit your setup

```bash
git add .
git commit -m "customize qua qua teams template"
git push origin main
```

## Optional knowledge layer

If you want stronger long-term searchable knowledge later, add a separate durable knowledge system such as GBrain.

Keep the layering clear:
- workspace for active execution
- memory files for continuity
- durable knowledge only when it is worth preserving separately

## Next steps

- Read [CUSTOMIZATION.md](CUSTOMIZATION.md)
- Read [EXAMPLES.md](EXAMPLES.md)
- Start with real tasks before adding more structure

## Troubleshooting

### Delegation feels clunky
- delegate less often
- narrow sub-agent scope
- improve handoff format

### Voice feels inconsistent
- tighten `SOUL.md`
- make Quả Quả rewrite final outputs
- reduce raw specialist text in final replies

### Memory feels messy
- keep daily notes raw
- promote only lasting context into curated memory
- avoid storing transient execution detail as durable knowledge
