---
tags: [ai-agents, memory, cognitive-science]
sources: [Build Agents that never forget.md]
created: 2026-04-14
updated: 2026-04-14
---

# Semantic Memory

One of three divisions of long-term memory in [[Lilian Weng]]'s cognitive-science framing of [[Agent Memory]]. Stores **general facts and concepts**, stripped of the time and context of any specific episode.

> Example: "PostgreSQL is a relational database."

## Role in Agents

- Holds the background knowledge an agent uses to reason about new situations.
- Produced from [[Episodic Memory]] via [[Memory Consolidation]] — e.g., "users consistently prefer executive summaries" emerges from dozens of individual episodes.
- In graph-based memory systems, semantic facts typically become **nodes and edges** (entities and relationships) rather than time-stamped log entries; this is what makes [[Knowledge Graph for Agent Memory]] possible.

## Related

- [[Episodic Memory]]
- [[Procedural Memory]]
- [[Memory Consolidation]]
- [[Agent Memory]]
