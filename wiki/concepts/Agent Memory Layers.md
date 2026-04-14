---
tags: [ai-agents, memory, architecture]
sources: [Build Agents that never forget.md]
created: 2026-04-14
updated: 2026-04-14
---

# Agent Memory Layers

The evolutionary ladder of agent-memory implementations. Each layer fixes the previous layer's failure mode and exposes a deeper one.

## Layer 0 — Stateless

Raw LLM call with no memory. Every API call starts fresh. The "memory" felt in chat UIs is an illusion produced by re-sending prior turns.

**Fails at:** anything multi-turn.

## Layer 1 — Python List

In-process conversation history re-shipped with each call.

**Fixes:** multi-turn coherence.
**Fails at:**
- Unbounded growth — context ceiling drops oldest messages silently (strict chronological order, no prioritization).
- No persistence — everything dies with the Python process.

## Layer 2 — Markdown Files on Disk

Human-readable, Git-friendly, editable by hand. [[Claude Code]]'s `CLAUDE.md` and `MEMORY.md` pattern is the canonical example.

**Fixes:** persistence across restarts. Great for prototyping and when fact count is small.
**Fails at:** retrieval at scale. With thousands of facts totaling 500K+ tokens on disk against a 128K window, the agent can no longer load everything. Keyword search (`grep`) can't bridge synonyms, paraphrases, or connections across facts — "cloud migration" won't match "migrating to a new AWS region." **Storage without intelligent retrieval is a library with no catalog.**

## Layer 3 — Vector Search (Embeddings)

Chunk, embed, cosine-similarity search. Solves the synonym problem: "database" matches "PostgreSQL" because their vectors are close in embedding space.

**Fixes:** semantic retrieval.
**Fails at:** relational, multi-hop questions. Each fact is an isolated point in embedding space. The *connective* facts that bridge entities are invisible to pure similarity.

> **The canonical failure:** given facts "Alice is tech lead on Project Atlas", "Project Atlas uses PostgreSQL", "The PostgreSQL cluster had an outage Tuesday" — the query "Was Alice's project affected by Tuesday's outage?" ranks facts 1 and 3 high but misses fact 2 (the bridge), because the bridge mentions neither Alice nor Tuesday.

Business knowledge is inherently relational (people → teams → projects → systems → incidents). Any query crossing two or more hops exceeds flat vector retrieval.

## Layer 4 — Graph + Vector Hybrid

Combine semantic retrieval with explicit relationships. Entities and relations become graph nodes and edges; every node also has an embedding. See [[Dual Index Retrieval]] for the mechanics and [[Knowledge Graph for Agent Memory]] for the data model.

**Fixes:** multi-hop reasoning while preserving semantic search.
**Still requires:** [[Memory Consolidation]] so the graph learns from its own usage rather than accumulating stale nodes.

## The Capability Matrix

| Layer | Multi-turn | Persistent | Semantic | Relational |
|---|---|---|---|---|
| Python list | ✅ | ❌ | ❌ | ❌ |
| Markdown | ✅ | ✅ | ❌ | ❌ |
| Vector | ✅ | ✅ | ✅ | ❌ |
| Graph + Vector | ✅ | ✅ | ✅ | ✅ |

A production memory layer needs all four in one system.

## Related

- [[Agent Memory]]
- [[Dual Index Retrieval]]
- [[Knowledge Graph for Agent Memory]]
- [[Lost in the Middle]]
- [[Context Management]]
