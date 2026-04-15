# Sub-Agent Playbook

Practical rules for using sub-agents inside the **Quả Quả + Teams** template.

## Default stance

Sub-agents are useful when they reduce cognitive load or increase quality.
They are not useful when they only add ceremony.

## Good uses for sub-agents

Use sub-agents when work is:
- parallelizable
- bounded and easy to scope
- better with specialist isolation
- large enough that direct execution would be noisy
- worth reviewing before it reaches the user

Good examples:
- research fan-out
- codebase scanning
- implementation of a clearly defined chunk
- independent review or QA
- packaging artifacts from an already clear plan

## Bad uses for sub-agents

Avoid sub-agents when:
- the task is tiny
- the work depends on one continuous judgment loop
- the handoff would be longer than the work itself
- the user needs one strong answer more than multiple perspectives

## Handoff contract

Every sub-agent task should include:
- **Task**
- **Context**
- **Goal**
- **Constraints**
- **Output**
- **Stop condition**

The stop condition matters. It prevents fake confidence and unnecessary wandering.

## Delivery rule

Sub-agents can hand artifacts or summaries to Quả Quả or to another specialist when the workflow explicitly needs it.
Default final delivery to the user still belongs to Quả Quả.

## Review rule

Before using a sub-agent result, Quả Quả should check:
1. did it answer the assigned question
2. is there enough evidence
3. is anything risky or uncertain
4. does it conflict with another result
5. should it be rewritten into a cleaner final answer

## Escalation rule

Escalate instead of guessing when:
- scope is ambiguous in a risky way
- the task needs a decision outside assigned authority
- required tools or context are missing
- a blocker persists beyond the expected bound

## Practical progression

Good adoption order:
1. Quả Quả only
2. Quả Quả plus one bounded specialist at a time
3. parallel specialists for clearly separable work
4. persistent specialists only after repeated real need

## Bottom line

Sub-agents should feel like clean invisible support beams.
The user should mostly experience better work, not more workflow theater.
