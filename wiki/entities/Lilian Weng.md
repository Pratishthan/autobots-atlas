---
tags: [person, ai-agents, research]
sources: [Build Agents that never forget.md]
created: 2026-04-14
updated: 2026-04-14
---

# Lilian Weng

Researcher best known in the agent-building community for her 2023 formulation that has become a default framework for agentic systems:

> **Agent = LLM + Memory + Planning + Tool Use**

The four co-equal pillars position [[Agent Memory]] alongside the model itself, rather than as an afterthought of the prompt.

## Cognitive-Science Taxonomy

Her framing borrows the human-memory split from cognitive science and maps each system onto a component in modern agent architectures:

- **Sensory memory** → short-lived perceptual buffer; only attended portions move forward.
- **Working memory** → active reasoning slot, roughly 7±2 items (Miller, 1956).
- **Long-term memory** → durable storage with no practical capacity ceiling; retrieval is the bottleneck.

Long-term memory further splits into [[Episodic Memory]], [[Semantic Memory]], and [[Procedural Memory]], bridged by [[Memory Consolidation]].

## Related

- [[Agent Memory]]
- [[Build Agents That Never Forget]]
