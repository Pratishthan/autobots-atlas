---
tags: [organization, ai-agents, llm-tooling]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# OpenAI

AI company; creator of the GPT model family, the Agents SDK, and the Codex coding agent.

## Agents SDK

The Agents SDK implements the [[Agent Harness]] through a `Runner` class with three execution modes: async, sync, and streamed. It is "code-first": workflow logic is expressed in native Python rather than graph DSLs.

Tool support spans three categories:
- **Function tools** — via `@function_tool` decorator
- **Hosted tools** — WebSearch, CodeInterpreter, FileSearch
- **MCP server tools** — Model Context Protocol integrations

**Guardrail architecture** has three levels:
- Input guardrails (run on first agent)
- Output guardrails (run on final output)
- Tool guardrails (run on every tool invocation)
- "Tripwire" mechanism halts the agent immediately when triggered

**State management** offers four mutually exclusive strategies: application memory, SDK sessions, server-side Conversations API, or lightweight `previous_response_id` chaining.

## Codex Harness

The Codex harness extends the Agents SDK with a three-layer architecture:
1. **Codex Core** — agent code + runtime
2. **App Server** — bidirectional JSON-RPC API
3. **Client surfaces** — CLI, VS Code, web app

All surfaces share the same harness. This explains why "Codex models feel better on Codex surfaces than a generic chat window."

**Prompt priority stack** (highest to lowest): server-controlled system message → tool definitions → developer instructions → user instructions (cascading AGENTS.md files, 32 KiB limit) → conversation history.

## Terminology

OpenAI's Codex team explicitly equates "agent" and "harness" to refer to the non-model infrastructure that makes the LLM useful.

## Related

- [[Agent Harness]]
- [[Orchestration Loop]]
- [[Subagent Orchestration]]
