# OpenClaw Multi-Agent Config

Concrete OpenClaw runtime config for the **Quả Quả + Teams** pattern.

## Goal

Provide one user-facing orchestrator plus bounded native sub-agents:
- `quaqua` is the default orchestrator
- `mat-cu`, `tieu-mi`, `ti-can`, `tieu-hoa` are explicit spawn targets
- delegation is explicit and shallow
- final delivery remains centralized through Quả Quả

## Recommended config block

Use this as the target shape in `~/.openclaw/openclaw.json`.

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
      workspace: "/root/.openclaw/workspace",
      model: {
        primary: "openai-codex/gpt-5.4",
        fallbacks: ["llmtinhtute/claw"],
      },
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

    list: [
      {
        id: "quaqua",
        default: true,
        name: "Quả Quả",
        workspace: "/root/.openclaw/workspace",
        agentDir: "/root/.openclaw/agents/quaqua/agent",
        identity: { name: "Quả Quả", emoji: "🍑" },
        subagents: {
          allowAgents: ["mat-cu", "tieu-mi", "ti-can", "tieu-hoa"],
          requireAgentId: true,
        },
      },
      {
        id: "mat-cu",
        name: "Mắt Cú",
        workspace: "/root/.openclaw/workspace",
        agentDir: "/root/.openclaw/agents/mat-cu/agent",
        identity: { name: "Mắt Cú", emoji: "🦉" },
      },
      {
        id: "tieu-mi",
        name: "Tiểu Mỉ",
        workspace: "/root/.openclaw/workspace",
        agentDir: "/root/.openclaw/agents/tieu-mi/agent",
        identity: { name: "Tiểu Mỉ", emoji: "🐱" },
      },
      {
        id: "ti-can",
        name: "Tí Cận",
        workspace: "/root/.openclaw/workspace",
        agentDir: "/root/.openclaw/agents/ti-can/agent",
        identity: { name: "Tí Cận", emoji: "🐭" },
      },
      {
        id: "tieu-hoa",
        name: "Tiểu Hoa",
        workspace: "/root/.openclaw/workspace",
        agentDir: "/root/.openclaw/agents/tieu-hoa/agent",
        identity: { name: "Tiểu Hoa", emoji: "🦋" },
      },
    ],
  },

  tools: {
    profile: "coding",
    subagents: {
      tools: {
        deny: ["sessions_list", "sessions_history"],
      },
    },
  },
}
```

## Why this config is the right fit

### `requireAgentId: true`
- forces explicit routing
- keeps Quả Quả in control
- avoids vague anonymous child sessions

### `maxSpawnDepth: 1`
- allows Quả Quả -> specialist
- prevents specialist -> specialist -> specialist chains by default
- matches the orchestrator-first design

### `maxConcurrent: 4`
- enough for practical fan-out
- still conservative for debugging and review

### shared workspace + separate `agentDir`
- one repo, one assistant system
- separate auth/session state per agent id
- easy to isolate further later if needed

## Recommended model stance

Start simple:
- let all specialists inherit the main default model first
- optimize later only if cost or speed becomes important

Possible later tuning:
- `mat-cu`: cheaper research/summarization model
- `tieu-mi`: lighter operational model
- `ti-can`: stronger coding model
- `tieu-hoa`: visual/design-friendly model if available

## Current live config check

The live runtime at `/root/.openclaw/openclaw.json` already matches the important sub-agent structure on these points:
- `quaqua` exists and is default
- all four specialists exist as explicit agent ids
- `requireAgentId: true`
- `maxSpawnDepth: 1`
- sub-agent tool deny list includes `sessions_list` and `sessions_history`

## Validation checklist

A correct configuration should satisfy all of these:

### Structure
- [ ] `quaqua` is present in `agents.list`
- [ ] `quaqua.default` is `true`
- [ ] `mat-cu`, `tieu-mi`, `ti-can`, `tieu-hoa` all exist in `agents.list`
- [ ] each specialist has its own `agentDir`
- [ ] shared workspace path is intentional

### Delegation control
- [ ] `agents.defaults.subagents.allowAgents` lists exactly the specialist ids
- [ ] `agents.defaults.subagents.requireAgentId` is `true`
- [ ] `agents.defaults.subagents.maxSpawnDepth` is `1`
- [ ] `maxConcurrent` and timeouts are set consciously

### Tool safety
- [ ] `tools.subagents.tools.deny` includes session-browsing tools not needed by leaf workers
- [ ] sandbox stance is intentional for child runs

### UX consistency
- [ ] specialists are documented as internal workers, not user-facing bots
- [ ] final answer flow is still Quả Quả -> user
- [ ] sub-agent prompts ask for scoped internal outputs, not final chat replies

## Validation commands

Use these checks on a real machine:

```bash
python3 - <<'PY'
import json
p='/root/.openclaw/openclaw.json'
obj=json.load(open(p))
ids=[a.get('id') for a in obj.get('agents',{}).get('list',[])]
print('default=', [a.get('id') for a in obj['agents']['list'] if a.get('default')])
print('ids=', ids)
print('requireAgentId=', obj['agents']['defaults']['subagents']['requireAgentId'])
print('maxSpawnDepth=', obj['agents']['defaults']['subagents']['maxSpawnDepth'])
print('allowAgents=', obj['agents']['defaults']['subagents']['allowAgents'])
print('toolDeny=', obj.get('tools',{}).get('subagents',{}).get('tools',{}).get('deny'))
PY
```

```bash
openclaw status
```

## Important note about runtime validation

Config validation and runtime validation are different.

- **Config validation** asks: is the multi-agent structure correct?
- **Runtime validation** asks: can this specific gateway/session state actually execute child spawns right now?

A gateway auth or pairing problem can block runtime spawn tests even when the multi-agent config itself is correct.
That does not invalidate the architecture or the config shape.

## Final recommendation

Use this stack as the stable baseline:
- Quả Quả as the only user-facing orchestrator
- four explicit specialist ids
- explicit delegation via `requireAgentId`
- shallow bounded sub-agent execution
- centralized review and delivery
