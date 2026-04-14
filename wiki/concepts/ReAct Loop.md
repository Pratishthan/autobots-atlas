---
tags: [ai-agents, orchestration, llm-tooling]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# ReAct Loop

The Thought-Action-Observation (TAO) cycle. The core pattern underlying the [[Orchestration Loop]] of an [[Agent Harness]].

**Re**asoning + **Act**ion = ReAct.

## Cycle

1. **Thought** — model reasons about what to do
2. **Action** — model selects and calls a tool
3. **Observation** — tool result is returned to the model
4. Repeat

## ReAct vs. Plan-and-Execute

Two dominant orchestration strategies:

| | ReAct | Plan-and-Execute |
|---|---|---|
| Structure | Interleaves reasoning and action at every step | Separates planning phase from execution phase |
| Flexibility | High — can adapt mid-task | Lower — plan is made upfront |
| Per-step cost | Higher — model reasons each step | Lower — execution phase is more direct |
| Speed | Slower | LLMCompiler reports **3.6x speedup** over sequential ReAct |

## Framework Context

Most frameworks implement ReAct as their default [[Orchestration Loop]]:
- [[Anthropic]] Claude Agent SDK: "dumb loop" driven by model tool calls
- [[OpenAI]] Agents SDK: `Runner` class
- LangGraph ([[LangChain]]): `llm_call` → `tool_node` → conditional routing

## Related

- [[Orchestration Loop]]
- [[Agent Harness]]
