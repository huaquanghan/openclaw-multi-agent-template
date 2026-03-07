# Customization Guide

How to customize this template for your specific needs.

## Table of Contents

1. [Adding New Agents](#adding-new-agents)
2. [Modifying Workflows](#modifying-workflows)
3. [Custom Tools](#custom-tools)
4. [Changing Team Structure](#changing-team-structure)
5. [Advanced Configuration](#advanced-configuration)

## Adding New Agents

To add a new agent to your team:

### 1. Create Agent Directory

```bash
mkdir -p agents/new-agent-name
touch agents/new-agent-name/{SOUL.md,USAGE.md,CONFIG.md}
```

### 2. Write SOUL.md

Define the agent's personality:

```markdown
# SOUL.md - Agent Name

**Name:** [Name]
**Creature:** [What they are]
**Emoji:** [Emoji]
**Role:** [Their role]

## Personality
[Define traits, communication style]

## Responsibilities
[What they do]

## When to Escalate
[When to ask for help]
```

### 3. Write USAGE.md

Document how to use the agent:

```markdown
# USAGE.md - How to Use [Agent]

## When to Call
[Appropriate tasks]

## How to Delegate
[Delegation format]

## Example Requests
[Sample prompts]
```

### 4. Write CONFIG.md

Set technical configuration:

```markdown
# CONFIG.md - [Agent] Configuration

## Settings
```yaml
name: [Name]
role: [Role]
emoji: [Emoji]
```

## Capabilities
- [Capability 1]
- [Capability 2]
```

### 5. Update Team Documentation

Add the new agent to:
- `AGENTS.md` - Team roster
- `ORCHESTRATION_WORKFLOW.md` - Decision matrix

## Modifying Workflows

### Changing the Orchestration Flow

Edit `ORCHESTRATION_WORKFLOW.md`:

1. Modify the workflow diagram
2. Update step descriptions
3. Adjust the decision matrix
4. Add/remove communication patterns

### Custom Task Patterns

Add your own patterns:

```markdown
## My Custom Pattern

1. **Step 1** - [Description]
2. **Step 2** - [Description]
3. **Step 3** - [Description]

### When to Use
[Appropriate scenarios]

### Example
[Concrete example]
```

## Custom Tools

### Adding Tool Documentation

Update `TOOLS.md` with your tools:

```markdown
### [Tool Name]

**Purpose:** [What it does]
**Usage:** [How to use it]
**Notes:** [Important details]
```

### Agent-Specific Tools

Add to agent's `CONFIG.md`:

```markdown
## Tools

### [Tool Name]
- Command: [How to invoke]
- Config: [Configuration]
```

## Changing Team Structure

### Removing Agents

1. Delete the agent's folder: `rm -rf agents/agent-name/`
2. Remove from `AGENTS.md`
3. Update `ORCHESTRATION_WORKFLOW.md` decision matrix
4. Commit changes

### Renaming Agents

1. Rename folder: `mv agents/old-name agents/new-name`
2. Update all references in documentation
3. Update `AGENTS.md`
4. Update `ORCHESTRATION_WORKFLOW.md`

### Changing Roles

1. Edit the agent's `SOUL.md`
2. Update responsibilities
3. Update `USAGE.md` with new capabilities
4. Update team documentation

## Advanced Configuration

### Custom Response Formats

Define custom formats in agent's `CONFIG.md`:

```markdown
## Output Formats

### My Custom Format
```
[Template]
```
```

### Integration Settings

Configure external integrations:

```markdown
## Integrations

### [Service]
```yaml
enabled: true
api_key: ${ENV_VAR}
settings:
  option: value
```
```

### Memory Management

Customize memory behavior:

```markdown
## Memory

### Daily Notes
- Location: `memory/`
- Format: [Your format]
- Retention: [How long to keep]

### Long-term
- Location: `MEMORY.md`
- Update frequency: [How often]
```

## Theming

### Visual Identity

Customize the team's visual identity:

1. Create `assets/` folder
2. Add logos, avatars, etc.
3. Reference in `IDENTITY.md`
4. Update agent emojis if desired

### Documentation Style

Make the docs your own:

- Change color references
- Update examples to match your domain
- Add your own best practices
- Include your own templates

## Best Practices

### Keep It Simple
- Don't over-engineer
- Start with defaults
- Add complexity only when needed

### Document Changes
- Update docs when you customize
- Note why you made changes
- Keep a changelog

### Test Iteratively
- Make small changes
- Test thoroughly
- Adjust based on results

### Share Learnings
- Document what works
- Note what doesn't
- Help others learn from your experience

## Examples

### Example: Adding a Data Analyst Agent

```bash
mkdir -p agents/data-whiz
cat > agents/data-whiz/SOUL.md << 'EOF'
# SOUL.md - Data Whiz

**Name:** Data Whiz
**Creature:** Fox - clever, analytical
**Emoji:** 🦊
**Role:** Data analyst, insights generator
...
EOF
```

### Example: Custom Workflow for Content Creation

```markdown
## Content Creation Workflow

1. **Research** (🦉 Mắt Cú)
   - Topic research
   - Competitor analysis
   
2. **Outline** (🐯 Cọp)
   - Structure content
   - Assign sections
   
3. **Draft** (🐭 Tí Cận)
   - Write content
   - Add code examples
   
4. **Visuals** (🦋 Tiểu Hoa)
   - Create diagrams
   - Design graphics
   
5. **Review** (🐯 Cọp)
   - Final edit
   - Publish
```

---

Remember: This template is a starting point. Make it yours!