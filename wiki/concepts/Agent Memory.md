---
tags: [ai-agents, memory, llm-tooling]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Agent Memory

One of the 12 components of the [[Agent Harness]]. Memory operates at multiple timescales.

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
- [[Context Management]]
- [[Beren Millidge]]
- [[Claude Code]]
