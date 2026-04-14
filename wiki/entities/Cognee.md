---
tags: [tool, ai-agents, memory, knowledge-graphs, open-source]
sources: [Build Agents that never forget.md]
created: 2026-04-14
updated: 2026-04-14
---

# Cognee

Open-source knowledge engine for [[Agent Memory]]. Combines three storage paradigms behind a small async API:

- **Relational store** — provenance (where data came from, when ingested, who has access)
- **Vector store** — semantics (meaning and similarity)
- **Graph store** — relationships between entities

Default embedded stack is **SQLite + LanceDB + Kuzu** (file-based, no Docker). Production deployments swap in Postgres, Qdrant/Pinecone/pgvector, and Neo4j/FalkorDB/Neptune respectively.

## Pipeline Stages

`cognify()` runs a multi-stage pipeline:

1. Document classification by type and domain
2. Permission checking for multi-tenant access
3. Chunk extraction respecting paragraph structure
4. Entity and relationship extraction via LLM, with content-hash deduplication
5. Summary generation
6. Dual indexing into both vector and graph stores — the technical basis of [[Dual Index Retrieval]]

`memify()` is an RL-inspired optimization pass over the graph — strengthening paths that led to good retrieval, pruning stale nodes, auto-tuning edge weights, and deriving implicit facts.

## Relevance to This Wiki

Cognee is cited in [[Build Agents That Never Forget]] as a concrete implementation of the graph-vector hybrid pattern for agent memory. It illustrates — rather than defines — [[Dual Index Retrieval]] and the three-store architecture.

## Related

- [[Agent Memory]]
- [[Dual Index Retrieval]]
- [[Knowledge Graph for Agent Memory]]
- [[Build Agents That Never Forget]]
