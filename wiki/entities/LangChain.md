---
tags: [organization, ai-agents, llm-tooling, orchestration]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# LangChain

AI tooling company; creators of the LangChain framework, LangGraph, and Deep Agents. [[Vivek Trivedy]] is a notable team member.

## TerminalBench Result

LangChain changed only the infrastructure wrapping their LLM (same model, same weights) and jumped from outside the top 30 to rank 5 on [[TerminalBench]] 2.0. This is the primary empirical evidence cited for the importance of [[Agent Harness]] quality independent of model capability.

## LangGraph

LangGraph models the [[Agent Harness]] as an explicit state graph. Two nodes (`llm_call` and `tool_node`) connected by a conditional edge: if tool calls present, route to `tool_node`; if absent, route to END.

State is modeled as typed dictionaries flowing through graph nodes, with reducers merging updates. Checkpointing happens at super-step boundaries, enabling:
- Resume after interruptions
- Time-travel debugging

Memory uses namespace-organized JSON Stores.

LangGraph **evolved from** LangChain's `AgentExecutor`, which was deprecated in v0.2 because it was hard to extend and lacked multi-agent support.

## Deep Agents

LangChain's Deep Agents explicitly use the term "agent harness." Features: built-in tools, planning (`write_todos` tool), file systems for context management, subagent spawning, and persistent memory.

## Related

- [[Agent Harness]]
- [[Vivek Trivedy]]
- [[Orchestration Loop]]
- [[Subagent Orchestration]]
- [[TerminalBench]]
