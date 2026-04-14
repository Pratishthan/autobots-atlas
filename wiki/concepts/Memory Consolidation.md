---
tags: [ai-agents, memory, cognitive-science]
sources: [Build Agents that never forget.md]
created: 2026-04-14
updated: 2026-04-14
---

# Memory Consolidation

The bridge between [[Episodic Memory]] and [[Semantic Memory]] / [[Procedural Memory]]: **repeated specific events distill into general knowledge**.

## Why It Matters for Agents

An agent that notices "users consistently prefer executive summaries" across dozens of interactions should convert that observation into a reusable rule. Without consolidation, the agent replays individual episodes rather than learning from them — episodic recall becomes a log, not intelligence.

Consolidation is what turns a memory system from **storage of events** into **accumulated expertise**.

## Implementations

- **Manual** — a human edits distilled facts into a markdown memory file (e.g. `MEMORY.md` in [[Claude Code]]).
- **RL-inspired graph optimization** — passes like Cognee's `memify()` strengthen frequently-traversed edges, prune stale nodes, and derive implicit facts. See [[Cognee]] and [[Knowledge Graph for Agent Memory]].
- **Edge weight auto-tuning** — adjusting retrieval weights based on real usage so the graph develops its own sense of relevance over time.

## Related

- [[Episodic Memory]]
- [[Semantic Memory]]
- [[Procedural Memory]]
- [[Agent Memory]]
