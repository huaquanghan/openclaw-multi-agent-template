# OpenClaw Fully Sub-Agents Setup

How to run the **Quả Quả + Teams** template in a fully native OpenClaw sub-agent model.

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

## OpenClaw runtime defaults to aim for

Recommended starting config pattern:

```json5
{
  agents: {
    defaults: {
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

- `allowAgents`: restricts Quả Quả to known-safe specialist profiles
- `requireAgentId: true`: forces explicit routing instead of vague anonymous spawns
- `maxSpawnDepth: 1`: Quả Quả can spawn specialists, but specialists cannot spawn their own children yet
- `maxConcurrent: 4`: enough for practical fan-out without noisy over-parallelism
- `runTimeoutSeconds: 900`: keeps child runs bounded
- `archiveAfterMinutes: 60`: cleans up finished sessions automatically

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

## Memory and knowledge routing

Use the routing model from `docs/KNOWLEDGE_ROUTING.md`:
- workspace for active work
- memory files for continuity
- durable knowledge only for reusable stable knowledge

Specialists should not dump raw execution residue into long-term knowledge.

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

A fully sub-agent OpenClaw setup for this repo means:
- Quả Quả remains the orchestrator
- specialists exist as explicit spawn targets
- Quả Quả spawns them only when useful
- final delivery remains centralized
