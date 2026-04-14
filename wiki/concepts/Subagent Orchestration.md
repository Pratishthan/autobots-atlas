---
tags: [ai-agents, multi-agent, orchestration, llm-tooling]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Subagent Orchestration

One of the 12 components of the [[Agent Harness]]. Encompasses patterns for spawning and coordinating multiple agents.

## When to Use Multi-Agent

Both [[Anthropic]] and [[OpenAI]] recommend: **maximize a single agent first**. Multi-agent systems add overhead (extra LLM calls for routing, context loss during handoffs). Split only when:
- Tool overload exceeds ~10 overlapping tools, or
- Clearly separate task domains exist

## Claude Code Execution Models

[[Claude Code]] supports three subagent modes:
- **Fork** — byte-identical copy of parent context; agent shares full parent state
- **Teammate** — separate terminal pane; communicates via file-based mailbox
- **Worktree** — own git worktree; isolated branch per agent; enables parallel work without conflicts

## OpenAI Patterns

[[OpenAI]] Agents SDK supports:
- **Agents-as-tools** — specialist handles a bounded subtask and returns; parent retains control
- **Handoffs** — specialist takes full control; parent relinquishes

## LangGraph

LangGraph ([[LangChain]]) implements subagents as **nested state graphs** — a subagent is a subgraph with its own state, connected to the parent graph.

## AutoGen Patterns

[[AutoGen]] supports five orchestration patterns:
1. Sequential
2. Concurrent (fan-out/fan-in)
3. Group chat
4. Handoff
5. Magentic (manager agent with dynamic task ledger)

## CrewAI

[[CrewAI]] uses a Crew (collection of Agents) with a Flows layer for deterministic routing between crews.

## Context Cost of Subagents

Sub-agents explore extensively but should return only **1,000–2,000 token condensed summaries** to the parent agent. This is a key [[Context Management]] strategy.

## Related

- [[Agent Harness]]
- [[Claude Code]]
- [[OpenAI]]
- [[LangChain]]
- [[AutoGen]]
- [[CrewAI]]
- [[Context Management]]
