---
tags: [ai-agents, memory, llm-tooling]
sources: [The Anatomy of an Agent Harness.md, Build Agents that never forget.md]
created: 2026-04-13
updated: 2026-04-14
---

# Agent Memory

One of the 12 components of the [[Agent Harness]]. Memory operates at multiple timescales.

## Why Memory Is a First-Class Concern

LLMs are **stateless by design** — every API call starts fresh. The "memory" felt in chat is an illusion created by re-shipping conversation history. Without engineered memory, agents exhibit predictable failure modes: context amnesia, zero personalization, multi-step task failure, repeated mistakes, no knowledge accumulation, hallucination from gaps, and identity collapse.

Expanding the context window does not fix this. [[Lost in the Middle]] shows 30%+ accuracy drops on mid-window content even in 128K+ windows. Context is a shared budget; absence of persistence, prioritization, and salience makes raw length insufficient.

## Cognitive-Science Taxonomy ([[Lilian Weng]])

> **Agent = LLM + Memory + Planning + Tool Use**

Four co-equal pillars. Borrowing from cognitive science:

- **Sensory memory** — raw perceptual buffer, fraction-of-a-second. Maps to tool-call outputs and observations entering context.
- **Working memory** — active reasoning slot (Miller's 7±2). Maps to the current context window.
- **Long-term memory** — durable storage, no practical capacity limit. Retrieval is the bottleneck. Maps to external stores (files, vectors, graphs).

Long-term memory itself splits into three kinds, bridged by [[Memory Consolidation]]:

- [[Episodic Memory]] — specific past events
- [[Semantic Memory]] — general facts and concepts
- [[Procedural Memory]] — skills and workflows

## Implementation Layers

See [[Agent Memory Layers]] for the full progression: stateless → Python list → markdown files → vector search → graph+vector hybrid. Each layer fixes the previous pain and exposes a deeper one. Production memory needs **persistence + semantic understanding + relational reasoning** together — which is what [[Dual Index Retrieval]] over a [[Knowledge Graph for Agent Memory]] provides.

## Timescales

### Short-Term Memory
Conversation history within a single session. Lives in the context window (the "RAM" in [[Beren Millidge]]'s analogy).

### Long-Term Memory
Persists across sessions. Implementation varies by framework:

| Framework | Long-Term Memory Implementation |
|---|---|
| [[Anthropic]] / [[Claude Code]] | CLAUDE.md project files + auto-generated MEMORY.md files |
| LangGraph ([[LangChain]]) | Namespace-organized JSON Stores |
| [[OpenAI]] Agents SDK | Sessions backed by SQLite or Redis |

## Claude Code's Three-Tier Hierarchy

[[Claude Code]] implements a three-tier approach:
1. **Lightweight index** (~150 characters per entry) — always loaded into context
2. **Detailed topic files** — pulled in on demand
3. **Raw transcripts** — accessed via search only

This architecture minimizes context consumption while preserving access to full memory depth.

## Critical Design Principle

> The agent treats its own memory as a **"hint"** and verifies against actual state before acting.

Memory can become stale. A robust harness verifies claimed state (file existence, function signatures, etc.) before acting on remembered facts.

## [[Beren Millidge]]'s Analogy

Short-term memory (context window) = RAM. Long-term memory (external databases) = disk storage. The harness manages paging between the two.

## Related

- [[Agent Harness]]
- [[Agent Memory Layers]]
- [[Dual Index Retrieval]]
- [[Knowledge Graph for Agent Memory]]
- [[Memory Consolidation]]
- [[Context Management]]
- [[Lost in the Middle]]
- [[Lilian Weng]]
- [[Beren Millidge]]
- [[Claude Code]]
