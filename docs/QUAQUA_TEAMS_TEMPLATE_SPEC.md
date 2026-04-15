# Quả Quả + Teams Template Spec

## Goal

Turn this repository from a generic multi-agent template into a **replicable Quả Quả + Teams template**.

The target is not just “an orchestrator with helpers”. The target is a reusable base for creating more assistants that share the same spirit:

- **Quả Quả** as the central identity and orchestrator
- **teams** as the extension layer for specialist work
- optional implementation via sub-agents, persistent agents, or channel routing depending on the deployment

## Core framing

### Quả Quả

Quả Quả is the main assistant identity.

Responsibilities:

- own the relationship with the human
- maintain the tone, memory habits, and operating rules
- decide when to do work directly and when to delegate
- synthesize team outputs before replying
- protect quality, privacy, and coherence

### Teams

Teams are specialist capability clusters that extend Quả Quả.

Examples:

- Research team
- Build team
- Ops team
- Design / content team

Each team may be implemented in different ways:

- as lightweight role docs only
- as OpenClaw sub-agents for bounded tasks
- as persistent specialist agents for heavier setups

The framing should stay stable even when the runtime implementation changes.

## Design principles

1. **Identity first**
   The template should feel like Quả Quả before it feels like a systems diagram.

2. **Teams are modular**
   Teams should be add-on capability packs, not required complexity.

3. **Single-core by default**
   A user should be able to start with one Quả Quả and no heavy multi-agent setup.

4. **Scale path exists**
   The template should make it easy to grow into team-based orchestration later.

5. **Knowledge is layered**
   Workspace, memory, and long-term knowledge should have distinct roles.

## What to keep from the current repo

- orchestrator-first workflow
- clear handoff format
- checkpoints and escalation
- role-based task routing
- simple repo structure

## What to change

- replace the generic “Cọp and cubs” framing with **Quả Quả + Teams** framing
- shift the repo from “team template only” to “identity + teams + replication template”
- explain that teams can be implemented with sub-agents or persistent agents later
- document how to replicate a new Quả Quả from this base

## Proposed repository layers

### 1. Identity layer

Files:

- `SOUL.md`
- `IDENTITY.md`
- `USER.md`
- `AGENTS.md`
- `TOOLS.md`
- `HEARTBEAT.md`

Purpose:

- define who Quả Quả is
- define how Quả Quả relates to the human
- define workspace law and continuity

### 2. Teams layer

Files:

- `ORCHESTRATION_WORKFLOW.md`
- `agents/*/SOUL.md`
- `agents/*/USAGE.md`
- `agents/*/CONFIG.md`
- `agents/*/IDENTITY.md`

Purpose:

- define specialist team roles
- define delegation expectations
- define how Quả Quả routes work into teams

### 3. Replication layer

New docs to add over time:

- `docs/SETUP_QUAQUA_TEMPLATE.md`
- `docs/QUAQUA_TEAMS_TEMPLATE_SPEC.md`
- `docs/SUBAGENT_PLAYBOOK.md`
- `docs/KNOWLEDGE_ROUTING.md`

Purpose:

- let a human or another agent spin up a new Quả Quả cleanly
- explain what to customize first
- explain how teams evolve with runtime complexity

## Knowledge model for this template

This template should explicitly support a layered model:

- **workspace files** for active execution and local operating rules
- **memory files** for continuity and personal context
- **durable knowledge system** such as GBrain when the deployment needs a separate long-term knowledge layer

This should be documented as an optional but recommended upgrade path, not forced into the minimal template.

## Team implementation modes

The same Quả Quả + Teams framing can run in multiple modes:

### Mode 1: Quả Quả only

- one main assistant
- team roles exist mainly as thinking/routing aids

### Mode 2: Quả Quả + sub-agents

- Quả Quả remains user-facing
- specialists run as bounded workers

### Mode 3: Quả Quả + persistent team agents

- specialist agents have their own channels or long-lived contexts
- useful when stronger isolation is needed

## File map changes planned from this spec

### Immediate

- reframe `README.md` around Quả Quả + Teams
- update `SOUL.md` to Quả Quả identity
- update `AGENTS.md` to be both workspace law and team map
- update `ORCHESTRATION_WORKFLOW.md` to describe Quả Quả-led orchestration

### Next docs

- add `docs/SETUP_QUAQUA_TEMPLATE.md`
- add `docs/SUBAGENT_PLAYBOOK.md`
- add `docs/KNOWLEDGE_ROUTING.md`

## Bottom line

This repo should become a **template for replicating more Quả Quả instances**, with teams as a structured extension layer.

The template should preserve personality, continuity, and practical orchestration, while staying flexible about whether teams are implemented as docs, sub-agents, or persistent specialist agents.
