---
tags: [product, ai-agents, llm-tooling, multi-agent]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# AutoGen

Microsoft's conversation-driven [[Agent Harness]] framework, evolving into the Microsoft Agent Framework. Pioneered conversation-driven orchestration.

## Architecture

Three-layer structure:
- **Core** — base primitives
- **AgentChat** — conversation orchestration
- **Extensions** — integrations and plugins

## Orchestration Patterns

Supports five patterns:
1. **Sequential** — agents run in order
2. **Concurrent** — fan-out/fan-in parallel execution
3. **Group chat** — agents converse to reach consensus
4. **Handoff** — control passes to a specialist agent
5. **Magentic** — a manager agent maintains a dynamic task ledger, coordinating specialists

## Related

- [[Agent Harness]]
- [[Subagent Orchestration]]
