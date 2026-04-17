# OpenClaw Machine Config Example

Production-ready example aligned with the current phase 1 live machine setup.

## Purpose

This file is for the case where you want a copy-paste-ready starting block that matches the current machine's working phase 1 sub-agent structure.

It focuses on:
- the current live default agent staying on `main`
- Quả Quả naming/identity applied on that live default agent
- four explicit specialist agent ids
- bounded native sub-agent rules
- the same provider/model shape already used on this machine

## Copy-paste-ready block

Adapt paths, secrets, and channel tokens before using in another environment.

```json
{
  "agents": {
    "defaults": {
      "workspace": "/root/.openclaw/workspace",
      "models": {
        "openai-codex/gpt-5.4": {},
        "llmtinhtute/claw": {
          "alias": "claw"
        }
      },
      "model": {
        "primary": "openai-codex/gpt-5.4",
        "fallbacks": [
          "llmtinhtute/claw"
        ]
      },
      "subagents": {
        "allowAgents": [
          "mat-cu",
          "tieu-mi",
          "ti-can",
          "tieu-hoa"
        ],
        "requireAgentId": true,
        "maxSpawnDepth": 1,
        "maxConcurrent": 4,
        "maxChildrenPerAgent": 4,
        "runTimeoutSeconds": 900,
        "archiveAfterMinutes": 60
      }
    },
    "list": [
      {
        "id": "main",
        "default": true,
        "name": "Quả Quả",
        "workspace": "/root/.openclaw/workspace",
        "agentDir": "/root/.openclaw/agents/main/agent",
        "identity": {
          "name": "Quả Quả",
          "emoji": "🍑"
        },
        "subagents": {
          "allowAgents": [
            "mat-cu",
            "tieu-mi",
            "ti-can",
            "tieu-hoa"
          ],
          "requireAgentId": true
        }
      },
      {
        "id": "mat-cu",
        "name": "Mắt Cú",
        "workspace": "/root/.openclaw/workspace",
        "agentDir": "/root/.openclaw/agents/mat-cu/agent",
        "identity": {
          "name": "Mắt Cú",
          "emoji": "🦉"
        }
      },
      {
        "id": "tieu-mi",
        "name": "Tiểu Mỉ",
        "workspace": "/root/.openclaw/workspace",
        "agentDir": "/root/.openclaw/agents/tieu-mi/agent",
        "identity": {
          "name": "Tiểu Mỉ",
          "emoji": "🐱"
        }
      },
      {
        "id": "ti-can",
        "name": "Tí Cận",
        "workspace": "/root/.openclaw/workspace",
        "agentDir": "/root/.openclaw/agents/ti-can/agent",
        "identity": {
          "name": "Tí Cận",
          "emoji": "🐭"
        }
      },
      {
        "id": "tieu-hoa",
        "name": "Tiểu Hoa",
        "workspace": "/root/.openclaw/workspace",
        "agentDir": "/root/.openclaw/agents/tieu-hoa/agent",
        "identity": {
          "name": "Tiểu Hoa",
          "emoji": "🦋"
        }
      }
    ]
  },
  "session": {
    "dmScope": "per-channel-peer"
  },
  "tools": {
    "profile": "coding",
    "subagents": {
      "tools": {
        "deny": [
          "sessions_list",
          "sessions_history"
        ]
      }
    }
  }
}
```

## Why this block is production-ready for this machine

It matches the currently validated live config on these important points:
- `main` is still the live default agent in phase 1
- the live default agent is named Quả Quả
- specialist ids are explicit
- `requireAgentId` is enabled
- spawn depth is bounded to `1`
- sub-agent session-browsing tools are denied
- default model and fallback match the live machine's setup

## What phase 1 does not claim yet

This example intentionally does **not** claim that the live machine has already finished the phase 2 rename/migration to a separate `quaqua` default agent id.
That remains a later cleanup step if you want the runtime ids to match the template framing exactly.

## What this block intentionally does not include

To keep it reusable and safer, this example does not include the full machine file with secrets and channel tokens, such as:
- gateway tokens
- Telegram bot tokens
- plugin API keys
- Notion or TTS API keys
- full provider secret material

Those should stay in the real machine config, not in a reusable template doc.

## Merge guidance

If you are applying this to a real config:
1. keep existing channel and auth sections unless you are intentionally replacing them
2. merge the `agents`, `session`, and `tools.subagents` sections carefully
3. preserve existing provider definitions that your environment already uses
4. re-run validation after merging

## Validation commands

```bash
python3 - <<'PY'
import json
p='/root/.openclaw/openclaw.json'
obj=json.load(open(p))
print('default=', [a.get('id') for a in obj['agents']['list'] if a.get('default')])
print('ids=', [a.get('id') for a in obj['agents']['list']])
print('requireAgentId=', obj['agents']['defaults']['subagents']['requireAgentId'])
print('maxSpawnDepth=', obj['agents']['defaults']['subagents']['maxSpawnDepth'])
print('allowAgents=', obj['agents']['defaults']['subagents']['allowAgents'])
print('toolDeny=', obj.get('tools',{}).get('subagents',{}).get('tools',{}).get('deny'))
PY
```

```bash
openclaw status
```

## Final note

A config can be structurally correct even if a separate gateway/session auth problem temporarily blocks live spawn tests.
Treat:
- config correctness
- runtime health

as two separate validation layers.
