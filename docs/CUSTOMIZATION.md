# Customization Guide

How to customize this template without losing the **Quả Quả + Teams** structure.

## Table of Contents

1. [Customize the core identity](#customize-the-core-identity)
2. [Customize teams](#customize-teams)
3. [Modify workflows](#modify-workflows)
4. [Tools and local setup](#tools-and-local-setup)
5. [Knowledge and memory layers](#knowledge-and-memory-layers)
6. [Advanced structure](#advanced-structure)

## Customize the core identity

The most important customization is the root identity layer:
- `SOUL.md`
- `IDENTITY.md`
- `USER.md`
- `AGENTS.md`

If these files are weak or inconsistent, the whole template feels generic.

### Good rule
Make Quả Quả feel like one coherent assistant first. Only then expand team complexity.

## Customize teams

Each team folder in `agents/` is a capability pack.

### To add a new specialist

```bash
mkdir -p agents/new-specialist
touch agents/new-specialist/{SOUL.md,USAGE.md,CONFIG.md,IDENTITY.md}
```

### What each file should do

#### `SOUL.md`
Define the specialist's working personality.

#### `USAGE.md`
Explain when Quả Quả should call this specialist.

#### `CONFIG.md`
Keep runtime notes, constraints, and technical preferences.

#### `IDENTITY.md`
Keep quick metadata for roster readability.

### Example specialist

```markdown
# SOUL.md - Data Whiz

**Name:** Data Whiz
**Creature:** Fox
**Emoji:** 🦊
**Role:** Data analysis and insights

## Responsibilities
- analyze datasets
- summarize findings
- suggest follow-up questions

## Escalation
- ambiguous metrics
- low confidence data quality
- business decisions requiring user judgment
```

Then update:
- `AGENTS.md`
- `ORCHESTRATION_WORKFLOW.md`

## Modify workflows

### Default stance
Do not start by adding more steps. Start by clarifying when to:
- do work directly
- delegate to one specialist
- split work across specialists

### Good workflow edits
- tighten handoff format
- define review requirements
- add escalation triggers
- reduce unnecessary parallelism

### Example custom pattern

```markdown
## Research -> Build -> Review

1. Mắt Cú researches sources and constraints
2. Tí Cận implements based on that summary
3. Quả Quả reviews and synthesizes final output
```

### Example content flow

```markdown
## Content Creation Workflow

1. **Research** (🦉 Mắt Cú)
2. **Outline** (🍑 Quả Quả)
3. **Draft** (🐭 Tí Cận)
4. **Visuals** (🦋 Tiểu Hoa)
5. **Review** (🍑 Quả Quả)
```

## Tools and local setup

Use `TOOLS.md` for environment-specific notes only.

Examples:
- SSH hosts
- preferred services
- TTS voices
- local aliases
- internal naming conventions

Do not turn `TOOLS.md` into a general manual.

## Knowledge and memory layers

This template works best when the layers stay separate:

### Workspace
For active execution, drafts, checklists, and temporary project state.

### Memory files
For continuity, habits, and personal context.

### Durable knowledge layer
Optional, for systems like GBrain when you want separate long-term searchable knowledge.

### Good customization rule
If something is still changing every day, keep it in workspace or daily memory first.
Only promote it when it becomes reusable and stable.

## Advanced structure

### Remove teams
If you want a simpler setup:
1. keep Quả Quả as the only active runtime
2. leave team docs as optional references
3. simplify the workflow docs accordingly

### Rename teams
If the names do not fit your assistant:
1. rename the agent folder
2. update references in docs
3. keep responsibilities clearer than branding

### Add persistent specialists
Only do this when:
- repeated workload clearly justifies it
- isolation matters
- you are ready to manage more operational complexity

## Best practices

### Keep it simple
Start with one strong assistant voice.

### Delegate with intent
Sub-agents should exist because they help, not because they look impressive.

### Document why
When you change structure, note why the change helps.

### Test with real tasks
Use the template on actual work before adding more ceremony.

---

This template is meant to be shaped. Just keep the center of gravity clear: **Quả Quả first, teams second**.
