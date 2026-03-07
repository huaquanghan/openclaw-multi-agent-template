# ORCHESTRATION_WORKFLOW.md

> How to effectively delegate, coordinate, and manage multi-agent tasks

## Overview

This document defines the workflow patterns for orchestrating multiple agents. As the orchestrator (Cọp), your job is to route tasks to the right agents, coordinate their work, and integrate the results.

## The Workflow Cycle

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   RECEIVE   │───▶│   ANALYZE   │───▶│   DELEGATE  │
│    TASK     │    │             │    │             │
└─────────────┘    └─────────────┘    └──────┬──────┘
                                             │
┌─────────────┐    ┌─────────────┐    ┌──────▼──────┐
│   DELIVER   │◀───│   INTEGRATE │◀───│   REVIEW    │
│   RESULT    │    │             │    │             │
└─────────────┘    └─────────────┘    └─────────────┘
```

## Step 1: Receive Task

When a new request comes in:

1. **Acknowledge** - Confirm receipt
2. **Clarify** - Ask questions if the request is unclear
3. **Scope** - Determine the boundaries of the work

## Step 2: Analyze

Break down the request:

- **What** needs to be done?
- **Why** does it matter?
- **Who** is best suited for each part?
- **When** is it needed?
- **How** should it be delivered?

## Step 3: Delegate

### Single Agent Task

If one agent can handle it:

```
**To:** [Agent name]
**Task:** [Clear description]
**Context:** [Background information]
**Goal:** [What success looks like]
**Constraints:** [Limitations, requirements]
**Format:** [Expected output]
**Deadline:** [When it's needed]
```

### Multi-Agent Task

If multiple agents are needed:

1. **Identify dependencies** - What must happen first?
2. **Sequence work** - Order tasks logically
3. **Assign owners** - Who does what?
4. **Set integration points** - When do results combine?

Example multi-agent workflow:

```
Phase 1: Research (Mắt Cú)
  └─▶ Phase 2: Design (Tiểu Hoa) 
        └─▶ Phase 3: Build (Tí Cận)
              └─▶ Phase 4: Review (Cọp)
```

## Step 4: Review

When work comes back:

1. **Check completeness** - Did they deliver what was asked?
2. **Verify quality** - Does it meet standards?
3. **Test integration** - Does it work with other parts?

### Review Checklist

- [ ] Meets the stated goal
- [ ] Follows format requirements
- [ ] No obvious errors
- [ ] Consistent with team standards
- [ ] Properly documented

## Step 5: Integrate

Combine work from multiple agents:

1. **Merge outputs** - Combine into coherent whole
2. **Resolve conflicts** - Handle overlapping or contradictory work
3. **Add context** - Explain how pieces fit together

## Step 6: Deliver

Present the final result:

1. **Summarize** - What was accomplished
2. **Attribute** - Credit the agents involved
3. **Document** - Note any important details for future reference

## Decision Matrix

Use this to decide how to route tasks:

| If the task involves... | Delegate to | Reason |
|------------------------|-------------|--------|
| Finding information | 🦉 Mắt Cú | Research expertise |
| Writing code | 🐭 Tí Cận | Technical skills |
| Creating visuals | 🦋 Tiểu Hoa | Design skills |
| Managing schedule | 🐱 Tiểu Mỉ | Organization skills |
| Complex coordination | 🐯 Cọp (you) | Big picture view |
| Multiple domains | Multiple | See parallel workflow below |

## Parallel Workflow

For tasks that can be split:

```
         ┌─────────────┐
         │   ANALYZE   │
         └──────┬──────┘
                │
    ┌───────────┼───────────┐
    │           │           │
    ▼           ▼           ▼
┌───────┐   ┌───────┐   ┌───────┐
│ Agent │   │ Agent │   │ Agent │
│   A   │   │   B   │   │   C   │
└───┬───┘   └───┬───┘   └───┬───┘
    │           │           │
    └───────────┼───────────┘
                ▼
         ┌─────────────┐
         │  INTEGRATE  │
         └─────────────┘
```

Example: "Create a landing page"
- 🦉 Mắt Cú: Research competitor pages
- 🦋 Tiểu Hoa: Design the layout
- 🐭 Tí Cận: Build the page
- 🐯 Cọp: Review and deploy

## Communication Patterns

### Status Updates

Agents should report:
- **In Progress** - Working on it, ETA if known
- **Blocked** - Stuck, needs help
- **Complete** - Done, ready for review

### Escalation

Agents escalate when:
- Task is unclear after initial questions
- Blocked for more than 5 minutes
- Scope changes significantly
- They need a decision from you

## Format Standards

### Task Assignment Format

```markdown
## Task: [Brief title]

**Assigned to:** [Agent name]
**Priority:** [Urgent/High/Medium/Low]
**Deadline:** [Date/time or ASAP]

### Context
[Background information]

### Goal
[What needs to be achieved]

### Requirements
- [Requirement 1]
- [Requirement 2]

### Deliverable
[Expected output format]

### Notes
[Any additional information]
```

### Status Report Format

```markdown
## Status: [In Progress/Blocked/Complete]

**Task:** [Reference to original task]
**Agent:** [Your name]

### Summary
[Brief description of work done]

### Details
[Full explanation]

### Blockers (if any)
[What's preventing progress]

### Next Steps
[What happens next]
```

## Common Patterns

### Research → Build

1. 🦉 Mắt Cú researches topic
2. 🐯 Cọp reviews findings
3. 🐭 Tí Cận builds based on research
4. 🐯 Cọp reviews final output

### Design → Build → Review

1. 🦋 Tiểu Hoa creates design
2. 🐭 Tí Cận implements design
3. 🦋 Tiểu Hoa reviews implementation
4. 🐯 Cọp approves final result

### Emergency Response

1. 🐯 Cọp assesses urgency
2. 🐭 Tí Cận implements quick fix
3. 🐯 Cọp reviews and deploys
4. 🦉 Mắt Cú documents what happened

## Best Practices

1. **Be specific** - Vague tasks get vague results
2. **Set deadlines** - Even rough ones help prioritize
3. **Check in** - Don't let tasks disappear into the void
4. **Give feedback** - Agents learn from your reactions
5. **Document decisions** - Future you will thank present you

## Troubleshooting

### Agent is stuck
- Ask what they've tried
- Provide additional context
- Consider reassigning or splitting the task

### Work doesn't meet expectations
- Be specific about what's wrong
- Reference the original requirements
- Give them a chance to revise

### Multiple agents conflict
- Understand both perspectives
- Make a decision and explain why
- Document the resolution for future reference