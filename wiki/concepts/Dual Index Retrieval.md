---
tags: [ai-agents, memory, retrieval, knowledge-graphs, vector-search]
sources: [Build Agents that never forget.md]
created: 2026-04-14
updated: 2026-04-14
---

# Dual Index Retrieval

A hybrid retrieval pattern for [[Agent Memory]] in which **every entity is represented twice** — once as a node in a graph (with typed edges to other entities) and once as an embedding in a vector index. The two representations share identity: for any node `N`, there is exactly one embedding `E(N)` that refers to the same underlying thing.

This dual representation is the core trick that unifies semantic search and relational reasoning.

## The Problem It Solves

Neither index alone is sufficient for realistic agent queries:

- **Vector-only** retrieval is blind to the connective tissue between facts. Given "Alice leads Project Atlas" / "Project Atlas uses PostgreSQL" / "PostgreSQL had an outage Tuesday," the query *"Was Alice's project affected by Tuesday's outage?"* ranks the first and third facts high but misses the second — the bridge mentions neither Alice nor Tuesday. See [[Agent Memory Layers]] for the full failure analysis.
- **Graph-only** retrieval requires knowing the exact entity to start traversal from. Natural-language queries don't name graph nodes; they describe them in paraphrased, synonym-rich language.

Dual indexing lets retrieval enter through one modality and exit through the other.

## The Two Traversal Directions

### Vector-in, Graph-out

1. Embed the query.
2. Nearest-neighbor search in the vector index returns seed nodes semantically similar to the query.
3. From those seeds, traverse the graph `k` hops along relevant edge types, collecting neighbors.
4. Return a connected subgraph (with provenance) as retrieval context.

Good for: "what do you know about Alice?" — ambiguous entry, structured expansion.

### Graph-in, Vector-out

1. Anchor a known entity in the graph (e.g., resolved from session state).
2. Walk the graph to a neighborhood of candidate nodes.
3. Rank or filter the neighborhood by vector similarity to the query.
4. Return the semantically relevant neighbors.

Good for: "tell me more about what Alice has been working on lately" — precise entry, semantic narrowing.

## Why the Bridge Only Works with Both

The "bridge" fact (`Project Atlas uses PostgreSQL`) is low-similarity to the query *"Was Alice's project affected by Tuesday's outage?"* — it contains none of the query's salient terms. A pure vector search will under-rank it. But it is a **single edge hop** from both "Alice" and "PostgreSQL." Graph traversal surfaces it for free, because relevance in the graph is defined by **topology**, not **text similarity**.

Conversely, the graph alone doesn't know that "database" and "PostgreSQL" should be treated as near-synonyms for matching a user query. The vector index supplies that.

## Prerequisites

For dual indexing to work cleanly, the ingestion pipeline must:

1. **Extract entities and relationships** consistently — the LLM must produce the same canonical node for "Alice", "alice@acme.com", and "Alice Chen."
2. **Deduplicate via content hashing** — if the same entity appears across 50 documents, it must collapse to a single graph node with 50 inbound edges. Otherwise the agent sees 50 strangers named Alice.
3. **Co-embed nodes and chunks** — every graph node gets an embedding derived from its summary and context so vector and graph IDs resolve to the same conceptual entity.
4. **Chunk by structure**, not fixed size, so embeddings carry coherent meaning.

See [[Cognee]] for one implementation of this pipeline.

## Tuning Over Time

Dual indices are static by default, which is fine until usage patterns diverge from ingestion assumptions. [[Memory Consolidation]] closes the loop:

- Strengthen edge weights along paths that produced good retrievals.
- Prune stale nodes that haven't been touched.
- Derive implicit relationships as new edges.

The graph develops its own sense of relevance based on how the agent actually queries it, rather than on how a human modeled the schema on day one.

## Contrast with Alternatives

| Approach | Semantic | Multi-hop | Provenance |
|---|---|---|---|
| BM25 / keyword | ❌ | ❌ | ✅ |
| Vector only | ✅ | ❌ | Weak |
| Graph only | Limited | ✅ | ✅ |
| **Dual index (graph + vector)** | ✅ | ✅ | ✅ |

The three-store architecture (relational + vector + graph) generalizes this: the relational store supplies provenance, the vector store supplies semantics, and the graph store supplies relationships. Flattening any of them loses information that matters for retrieval accuracy.

## Related

- [[Agent Memory]]
- [[Agent Memory Layers]]
- [[Knowledge Graph for Agent Memory]]
- [[Memory Consolidation]]
- [[Cognee]]
