---
tags: [ai-agents, memory, knowledge-graphs]
sources: [Build Agents that never forget.md]
created: 2026-04-14
updated: 2026-04-14
---

# Knowledge Graph for Agent Memory

Using a graph — nodes for entities, typed edges for relationships — as the **relational layer** of an agent's long-term memory. The graph complements (rather than replaces) a vector store; together they form [[Dual Index Retrieval]].

## Why a Graph

Real-world knowledge is relational: people belong to teams, teams own projects, projects depend on systems, systems have incidents. Any agent query that crosses two or more hops ("Was Alice's project affected by Tuesday's outage?") exceeds what flat [[Semantic Memory]] retrieval alone can answer — the bridging facts are invisible to vector similarity. See [[Agent Memory Layers]] for the full progression.

## What Lives Where

- **Nodes** — entities (people, products, projects, systems, events). Each node typically carries a summary embedding so it also participates in the vector index.
- **Edges** — typed relationships (`works_on`, `depends_on`, `caused`, `manages`). Edge types shape which traversals are meaningful.
- **Edge weights** — usage-derived relevance signals (see [[Memory Consolidation]]).
- **Provenance** — a separate relational store typically records which source document asserted each edge, when, and under what access scope.

## Construction Pipeline

A typical ingest path (exemplified by [[Cognee]]):

1. Chunk source documents by paragraph/structure.
2. LLM-extract entities and relationships per chunk.
3. Deduplicate entities via content hashing so repeated mentions collapse to a single node.
4. Co-embed nodes and chunks so the vector index and graph resolve to the same conceptual identities.
5. Index incrementally — only new or updated sources get reprocessed.

## Relationship to Other Concepts

- Pairs with [[Dual Index Retrieval]] as the graph half of the hybrid.
- Natural home for consolidated [[Semantic Memory]] (facts as nodes/edges) and for linking to [[Episodic Memory]] (events as time-stamped nodes with edges to affected entities).
- Edge-weight learning over time is a form of [[Memory Consolidation]].

## Related

- [[Agent Memory]]
- [[Agent Memory Layers]]
- [[Dual Index Retrieval]]
- [[Memory Consolidation]]
- [[Cognee]]
