---
tags: [ai-agents, memory, knowledge-graphs, vector-search]
sources: [Build Agents that never forget.md]
created: 2026-04-14
updated: 2026-04-14
blog_seed: false
actionable: true
---

# Build Agents That Never Forget

**Source:** Build Agents that never forget.md
**Original URL:** https://x.com/akshay_pachaar/status/2043745099792953508
**Author:** [[Akshay Pachaar]]
**Published:** 2026-04-13
**Date ingested:** 2026-04-14
**Type:** article (long-form thread / essay)

## Summary

A first-principles walk through agent memory. The piece argues that LLMs are stateless by design and that the "memory" felt in chat is an illusion produced by re-sending conversation history. It traces the evolution of agent memory through four implementation layers — Python list → markdown files → vector search → graph+vector hybrid — and shows the failure mode each layer exposes. It grounds the design in cognitive science (Lilian Weng's framing of Agent = LLM + Memory + Planning + Tool Use; sensory/working/long-term memory; episodic/semantic/procedural split). It closes by introducing [[Cognee]] as one open-source implementation of the three-store pattern.

## Key Claims

- LLMs are stateless; chat memory is an engineering trick (re-sending history).
- Without engineered memory, agents fail in 7 predictable ways: context amnesia, zero personalization, multi-step failure, repeated mistakes, no knowledge accumulation, hallucination from gaps, identity collapse.
- Simply enlarging the context window does not solve memory. Accuracy drops over 30% when relevant information sits in the middle of a long context ([[Lost in the Middle]]).
- Context is a shared budget — system prompt, retrieved docs, history, and output compete for the same tokens.
- Lilian Weng's formulation: **Agent = LLM + Memory + Planning + Tool Use**.
- Long-term memory splits into [[Episodic Memory]], [[Semantic Memory]], and [[Procedural Memory]]; the bridge is [[Memory Consolidation]].
- Each memory-implementation layer fixes the prior layer's pain and reveals a deeper one:
  - **Python list** — multi-turn works but unbounded growth and no persistence.
  - **Markdown files** — persistence solved; retrieval collapses to keyword search, which cannot bridge synonyms or paraphrases. [[Claude Code]]'s `CLAUDE.md` / `MEMORY.md` is an example of this layer.
  - **Vector search** — semantic match works; multi-hop relational questions fail because connecting facts don't share query terms (the "Alice's project / Tuesday's outage" case).
  - **Graph + vector hybrid** — adds relational reasoning on top of semantic retrieval.
- A production-grade memory layer needs **persistence + semantic understanding + relational reasoning** together.
- The graph-vector bridge works because every graph node has a corresponding embedding — enter via vectors, traverse via edges, or the reverse (see [[Dual Index Retrieval]]).
- [[Cognee]] is one open-source implementation combining a relational store (provenance), vector store (semantics), and graph store (relationships) behind a small async API.

## Entities Mentioned

- [[Akshay Pachaar]] — author
- [[Lilian Weng]] — source of the cognitive-science-grounded agent framework cited
- [[Anthropic]] / [[Claude Code]] — cited for the `CLAUDE.md` / `MEMORY.md` markdown-memory pattern
- [[OpenAI]] — SDK used in example code
- [[Cognee]] — open-source knowledge-engine example of the three-store pattern

## Concepts Covered

- [[Agent Memory]] — extended with cognitive-science taxonomy and implementation layers
- [[Agent Memory Layers]] — the four-layer evolution (list → markdown → vector → graph+vector)
- [[Lost in the Middle]] — 30%+ accuracy drop on mid-window content
- [[Episodic Memory]], [[Semantic Memory]], [[Procedural Memory]] — long-term memory types
- [[Memory Consolidation]] — distillation of specific events into general knowledge
- [[Dual Index Retrieval]] — graph + vector hybrid; every node has an embedding
- [[Knowledge Graph for Agent Memory]] — graph as relational reasoning layer over agent facts
- [[Context Rot]] — this source corroborates the "lost in the middle" evidence
