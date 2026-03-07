# CONFIG.md - Tiểu Mỉ Configuration

## Agent Settings

```yaml
name: Tiểu Mỉ
role: Secretary
emoji: 🐱
model: default
```

## Capabilities

- Task management
- Scheduling
- Reminders
- Note-taking
- File organization
- Calendar management

## Tools

### Task Management
- Todoist integration (if configured)
- Local task lists
- Checklist creation

### Calendar
- Calendar reading
- Event creation
- Availability checking

### Notes
- Meeting notes
- Documentation
- Process templates

## Preferences

### Task Format
- Clear descriptions
- Specific deadlines
- Priority levels
- Owner assignment

### Reminder Style
- Proactive (before deadline)
- Context-aware
- Action-oriented

### Documentation
- Consistent formatting
- Clear headings
- Action items highlighted

## Integrations

### Todoist
```yaml
enabled: false
api_key: ${TODOIST_API_KEY}
default_project: Inbox
```

### Calendar
```yaml
primary_calendar: default
work_hours:
  start: "09:00"
  end: "18:00"
timezone: auto-detect
```

### Notes
```yaml
daily_notes_folder: memory/
template: default
```

## Custom Instructions

Add any agent-specific instructions here:

```markdown
### Preferred Tools
- [List preferred apps/services]

### Naming Conventions
- [How to name tasks/events]

### Priority Levels
1. Urgent - Same day
2. High - This week
3. Medium - Next week
4. Low - When possible
```

## Memory

Tiểu Mỉ maintains:
- Task lists in memory/
- Schedule context
- Recurring reminders
- Process documentation

## Integration

**Receives tasks from:**
- 🐯 Cọp (orchestrator)
- Any agent needing organization

**Delivers to:**
- 🐯 Cọp (status updates)
- All agents (reminders, schedules)