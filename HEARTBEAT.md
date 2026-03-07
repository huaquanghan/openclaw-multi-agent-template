# HEARTBEAT.md - Periodic Tasks

This file defines tasks to check during heartbeat polls.

## What is a Heartbeat?

Heartbeats are periodic check-ins (typically every 30 minutes) where the orchestrator reviews what needs attention. Unlike cron jobs, heartbeats can batch multiple checks together and use conversational context.

## When to Use Heartbeats vs Cron

**Use heartbeat when:**
- Multiple checks can batch together (inbox + calendar + notifications)
- You need conversational context from recent messages
- Timing can drift slightly (every ~30 min is fine)
- You want to reduce API calls by combining checks

**Use cron when:**
- Exact timing matters ("9:00 AM sharp every Monday")
- Task needs isolation from main session history
- One-shot reminders ("remind me in 20 minutes")
- Output should deliver directly to a channel

## Heartbeat Checklist

Edit this list based on your needs. Check 2-4 items per heartbeat, rotating through them:

### Communication
- [ ] Check emails for urgent messages
- [ ] Review chat notifications/mentions
- [ ] Check social media DMs/mentions

### Schedule
- [ ] Review calendar for upcoming events (next 24-48h)
- [ ] Check for meeting conflicts
- [ ] Send reminders for upcoming events

### Tasks
- [ ] Review task list for overdue items
- [ ] Check project deadlines
- [ ] Follow up on delegated tasks

### Information
- [ ] Check news/sources for relevant updates
- [ ] Review RSS feeds
- [ ] Monitor specific keywords/topics

### System
- [ ] Check system health/status
- [ ] Review logs for errors
- [ ] Verify backups completed

## Tracking State

Track your checks in `memory/heartbeat-state.json`:

```json
{
  "lastChecks": {
    "email": 1703275200,
    "calendar": 1703260800,
    "tasks": 1703188800,
    "news": 1703102400
  }
}
```

## When to Reach Out

**Notify the user when:**
- Important email arrived
- Calendar event coming up (< 2 hours)
- Overdue tasks need attention
- Something interesting found
- It's been > 8 hours since last contact

**Stay quiet (HEARTBEAT_OK) when:**
- Late night (23:00-08:00) unless urgent
- User is clearly busy
- Nothing new since last check
- You just checked < 30 minutes ago

## Proactive Work

During heartbeats, you can also:
- Read and organize memory files
- Check project status (git status, etc.)
- Update documentation
- Commit and push changes
- Review and update MEMORY.md

## Memory Maintenance

Periodically (every few days), use a heartbeat to:

1. Read through recent `memory/YYYY-MM-DD.md` files
2. Identify significant events, lessons, or insights
3. Update `MEMORY.md` with distilled learnings
4. Remove outdated info from MEMORY.md

Think of it like reviewing a journal and updating your mental model.

## Customization

Add your own periodic checks here:

```markdown
### My Custom Checks

- [ ] Check stock prices
- [ ] Monitor website uptime
- [ ] Review analytics dashboard
```

---

Remember: Be helpful without being annoying. Check in a few times a day, do useful background work, but respect quiet time.