---
tags: [product, ai-agents, llm-tooling, multi-agent]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# CrewAI

Role-based multi-agent [[Agent Harness]] framework. Structures agent systems around three primitives:

- **Agent** — the harness around the LLM, defined by role, goal, backstory, and tools
- **Task** — the unit of work
- **Crew** — the collection of agents

## Flows Layer

CrewAI's Flows layer adds a "deterministic backbone with intelligence where it matters" — manages routing and validation while Crews handle autonomous collaboration. This is a hybrid approach: structured control flow combined with autonomous agent execution.

## Related

- [[Agent Harness]]
- [[Subagent Orchestration]]
