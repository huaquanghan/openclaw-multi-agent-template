# OpenClaw AI-First Sub-Agent Setup

How to run the **Quả Quả + Teams** template in an **AI-first** OpenClaw model: start with one strong orchestrator, then add native sub-agents with explicit config.

## Target operating model

This template assumes one user-facing orchestrator:
- **Quả Quả** stays in the main session
- specialists are **spawned on demand** with `sessions_spawn`
- specialists do bounded work and return scoped results
- Quả Quả reviews and synthesizes the final answer

This is the default target model for the repo.

## Non-goals

This setup is **not** trying to create:
- always-on specialist bots talking to the user directly
- peer-to-peer team chat exposed to the user
- deep nested orchestration by default

Those can exist later, but they are not the starting architecture.

## Recommended starting shape

### Main session
- agent identity: Quả Quả
- role: orchestrator
- responsibilities: routing, review, synthesis, memory, final delivery

### Spawned specialists
- `mat-cu` for research, source gathering, comparisons, review support
- `tieu-mi` for notes, checklists, reminders, coordination artifacts
- `ti-can` for coding, debugging, implementation, ops work
- `tieu-hoa` for visuals, UI/UX, packaging

## Where the real config lives

For a real OpenClaw setup, the main config usually lives at:

- `~/.openclaw/openclaw.json`

This template repo gives you the workspace/persona/docs layer.
The OpenClaw config is the runtime layer that turns those docs into actual agent behavior.

## OpenClaw runtime defaults to aim for

Recommended starting config pattern:

```json5
{
  session: {
    scope: "per-sender",
    dmScope: "per-peer",
    threadBindings: {
      enabled: true,
      idleHours: 24,
      maxAgeHours: 0,
    },
  },

  agents: {
    defaults: {
      model: { primary: "openai-codex/gpt-5.4" },
      thinkingDefault: "medium",
      subagents: {
        allowAgents: ["mat-cu", "tieu-mi", "ti-can", "tieu-hoa"],
        requireAgentId: true,
        maxSpawnDepth: 1,
        maxConcurrent: 4,
        maxChildrenPerAgent: 4,
        runTimeoutSeconds: 900,
        archiveAfterMinutes: 60,
      },
    },
  },
}
```

## Why these defaults

- `session.scope` and `dmScope`: keep user/session routing predictable before adding more agent complexity
- `threadBindings`: useful global defaults, even if thread-bound specialist sessions stay optional
- `allowAgents`: restricts Quả Quả to known-safe specialist profiles
- `requireAgentId: true`: forces explicit routing instead of vague anonymous spawns
- `maxSpawnDepth: 1`: Quả Quả can spawn specialists, but specialists cannot spawn their own children yet
- `maxConcurrent: 4`: enough for practical fan-out without noisy over-parallelism
- `runTimeoutSeconds: 900`: keeps child runs bounded
- `archiveAfterMinutes: 60`: cleans up finished sessions automatically

## Recommended `agents.list` shape

A practical AI-first setup is to define Quả Quả plus specialist agent ids explicitly.

```json5
{
  agents: {
    list: [
      {
        id: "quaqua",
        default: true,
        name: "Quả Quả",
        workspace: "~/assistants/quaqua",
        agentDir: "~/.openclaw/agents/quaqua/agent",
        identity: { name: "Quả Quả", emoji: "🍑" },
        subagents: {
          allowAgents: ["mat-cu", "tieu-mi", "ti-can", "tieu-hoa"],
          requireAgentId: true,
        },
      },
      {
        id: "mat-cu",
        name: "Mắt Cú",
        workspace: "~/assistants/quaqua",
        agentDir: "~/.openclaw/agents/mat-cu/agent",
        identity: { name: "Mắt Cú", emoji: "🦉" },
      },
      {
        id: "tieu-mi",
        name: "Tiểu Mỉ",
        workspace: "~/assistants/quaqua",
        agentDir: "~/.openclaw/agents/tieu-mi/agent",
        identity: { name: "Tiểu Mỉ", emoji: "🐱" },
      },
      {
        id: "ti-can",
        name: "Tí Cận",
        workspace: "~/assistants/quaqua",
        agentDir: "~/.openclaw/agents/ti-can/agent",
        identity: { name: "Tí Cận", emoji: "🐭" },
      },
      {
        id: "tieu-hoa",
        name: "Tiểu Hoa",
        workspace: "~/assistants/quaqua",
        agentDir: "~/.openclaw/agents/tieu-hoa/agent",
        identity: { name: "Tiểu Hoa", emoji: "🦋" },
      },
    ],
  },
}
```

Notes:
- separate `agentDir` matters, because OpenClaw keeps auth and session state per agent id
- sharing one workspace is acceptable when you want one assistant system with one repo
- if a specialist needs stronger isolation later, move it to its own workspace then

## Model strategy

Recommended model policy:
- Quả Quả can stay on the higher-quality default model
- spawned specialists can use a cheaper or narrower model where appropriate

Examples:
- `mat-cu`: good summarization / research model
- `ti-can`: stronger coding model
- `tieu-mi`: lighter operational model
- `tieu-hoa`: visual-capable or design-friendly model if available

Start simple if needed: let children inherit Quả Quả's model first, then optimize later.

If cost or throughput starts to matter, set `agents.defaults.subagents.model` to a cheaper default and override only the specialists that need more power.

## Provider bootstrap example

If you are not using only built-in providers, add a provider block in `~/.openclaw/openclaw.json`.

```json5
{
  env: {
    OPENAI_API_KEY: "${OPENAI_API_KEY}",
  },

  agents: {
    defaults: {
      model: { primary: "openai/gpt-5-mini" },
      subagents: {
        model: "openai/gpt-5-mini",
      },
    },
    list: [
      {
        id: "quaqua",
        model: { primary: "openai/gpt-5" },
      },
      {
        id: "ti-can",
        model: { primary: "openai/gpt-5-mini" },
      },
    ],
  },
}
```

The principle is simple:
- better main model for Quả Quả
- cheaper or narrower defaults for spawned specialists
- override only the specialists that truly need it

## Tool and sandbox stance

AI-first here means: give Quả Quả and specialists enough tools to work, but keep the runtime conservative.

Suggested stance:

```json5
{
  tools: {
    profile: "coding",
    subagents: {
      tools: {
        deny: ["sessions_list", "sessions_history"],
      },
    },
  },

  agents: {
    defaults: {
      sandbox: {
        mode: "all",
      },
    },
    list: [
      {
        id: "quaqua",
        tools: {
          profile: "coding",
        },
      },
      {
        id: "ti-can",
        tools: {
          profile: "coding",
        },
      },
    ],
  },
}
```

Notes:
- default leaf sub-agents do not get session tools anyway when `maxSpawnDepth: 1`
- sandboxing is a good default for spawned workers
- keep elevated or broad host access tightly restricted

## Spawn pattern

Quả Quả should use `sessions_spawn` with explicit scope.

### Research example

```json
{
  "agentId": "mat-cu",
  "task": "Research the topic, compare the top options, cite sources, and return a concise decision brief.",
  "label": "research-brief",
  "runTimeoutSeconds": 900,
  "cleanup": "keep",
  "sandbox": "require"
}
```

### Build example

```json
{
  "agentId": "ti-can",
  "task": "Implement the agreed change, test the result, summarize the files changed and remaining risks.",
  "label": "build-task",
  "runTimeoutSeconds": 1800,
  "cleanup": "keep",
  "sandbox": "require"
}
```

### Design example

```json
{
  "agentId": "tieu-hoa",
  "task": "Create a concise design direction and deliver mockup notes or assets for implementation.",
  "label": "design-pass",
  "runTimeoutSeconds": 1200,
  "cleanup": "keep",
  "sandbox": "require"
}
```

## Handoff contract

Every spawned specialist task should specify:
- task
- context
- goal
- constraints
- expected output
- stop condition

Good child outputs are:
- concise
- artifact-oriented
- explicit about uncertainty
- easy for Quả Quả to integrate

## Announce and delivery details that matter

OpenClaw sub-agents always finish through an announce step.
That means the child session returns a result back into the requester chain.

Important practical rules:
- treat child output as internal orchestration output, not final user copy
- Quả Quả should rewrite or integrate before the user sees the final answer
- if a child should stay silent after completion, exact `NO_REPLY` or `ANNOUNCE_SKIP` suppresses announce output
- do not build poll loops around sub-agent completion; let completion events come back naturally

## Delivery rule

Specialists are not the user-facing voice.

Default rule:
- specialists return findings, artifacts, or implementation summaries
- Quả Quả absorbs those results
- Quả Quả sends the final answer to the user

## Announce behavior

OpenClaw sub-agents have an announce step on completion.
Design your child prompts so the child returns:
- a scoped result summary
- artifact references
- risks and open questions

Do **not** design child prompts as if they are writing directly to the user in their own separate persona.

The visible experience should still feel like Quả Quả orchestrated and integrated the work.

## Why maxSpawnDepth should start at 1

Even though OpenClaw can support nested orchestrator patterns with `maxSpawnDepth: 2`, the recommended starting point here is:
- main Quả Quả session
- direct spawned specialists only

This matches the intended architecture better:
- Quả Quả is the orchestrator
- specialists are workers
- no second hidden orchestrator unless the workload proves you need one later

## Escalation rules

A specialist should escalate instead of guessing when:
- scope is ambiguous in a risky way
- it needs authority outside the assigned bounds
- required tools or files are missing
- implementation risk is higher than expected

Quả Quả decides whether to:
- narrow the task
- ask the user
- spawn a second specialist for review
- continue directly

## Channel and thread-binding note

For most AI-first setups, you do **not** need thread-bound specialist sessions yet.
Start with normal `sessions_spawn` runs and centralized delivery.

Only add thread-bound child sessions when the channel/runtime genuinely benefits from them.

Current practical note from OpenClaw docs:
- Discord is the main channel with documented thread-bound sub-agent support
- if you want spawned sub-agents to auto-bind into Discord threads, enable `channels.discord.threadBindings.spawnSubagentSessions: true`
- for Telegram or simpler direct-chat setups, this is usually unnecessary at the beginning

## Memory and knowledge routing

Use the routing model from `docs/KNOWLEDGE_ROUTING.md`:
- workspace for active work
- memory files for continuity
- durable knowledge only for reusable stable knowledge

Specialists should not dump raw execution residue into long-term knowledge.

## AI-first rollout order

### Stage 0, single assistant first
- make Quả Quả good before anything else
- keep specialist docs as capability packs only

### Stage 1, explicit runtime config
- create `agents.list` entries for Quả Quả and each specialist id
- keep Quả Quả as the default agent
- make delegation explicit with `requireAgentId: true`

### Stage 2, bounded sub-agent work
- use `sessions_spawn` for research, build, review, or coordination bursts
- keep `maxSpawnDepth: 1`
- keep final synthesis centralized

### Stage 3, optimize cost and routing
- tune sub-agent model defaults
- add stricter tool policy per specialist if needed
- add thread bindings only for channels that really benefit

### Stage 4, only if proven necessary
- consider `maxSpawnDepth: 2`
- consider persistent specialists or channel-specific bindings
- consider separate workspaces for heavier specialists

## Validation checklist

A setup is considered working when all of these are true:

- [ ] Quả Quả can spawn each specialist by explicit `agentId`
- [ ] specialists stay bounded and do not behave like free-form bots
- [ ] specialist outputs come back as scoped findings or artifacts
- [ ] final user-facing reply still reads like Quả Quả
- [ ] memory and durable knowledge routing stay clean
- [ ] there is no need for persistent specialist sessions to do normal work

## Suggested rollout order

### Phase 1
- keep the current repo docs as the source of truth
- map each specialist to a real OpenClaw agent id
- set `requireAgentId: true`
- keep `maxSpawnDepth: 1`

### Phase 2
- test one specialist at a time with real tasks
- tighten prompts, timeouts, and model choices
- confirm Quả Quả integration quality

### Phase 3
- test 2-way fan-out, for example research plus build
- test build plus review
- document what task shapes work best

### Phase 4
- only if needed, consider `maxSpawnDepth: 2` for a deeper orchestrator pattern
- only if needed, consider persistent specialists for channels with thread support

## Bottom line

An AI-first OpenClaw setup for this repo means:
- Quả Quả remains the orchestrator
- OpenClaw config makes Quả Quả and specialists explicit agent ids
- specialists exist as bounded spawn targets, not free-floating bots
- Quả Quả spawns them only when useful
- final delivery remains centralized
