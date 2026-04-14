---
tags: [ai-agents, context-management, llm-tooling]
sources: [The Anatomy of an Agent Harness.md, Build Agents that never forget.md]
created: 2026-04-13
updated: 2026-04-14
---

# Context Rot

The degradation of LLM performance as a context window fills with low-signal content, or as key information is pushed into mid-window positions.

## Evidence

- **30%+ performance degradation** when key content falls in mid-window positions (Chroma research)
- Corroborated by Stanford's "Lost in the Middle" finding
- Affects even million-token context windows

## Mechanism

LLMs attend more strongly to content at the beginning and end of the prompt. Information in the middle is systematically under-attended. As a context window grows with tool outputs, observations, and intermediate steps, important information migrates toward the middle.

## Mitigations

See [[Context Management]] for production strategies:
- Compaction
- Observation masking
- Just-in-time retrieval
- Sub-agent delegation
- Structured note-taking

## Implications for Harness Design

Context rot is one of the core reasons the [[Agent Harness]] must actively manage context rather than simply appending all history. An agent that naively grows its context will degrade in performance over multi-step tasks.

## Related

- [[Lost in the Middle]]
- [[Context Management]]
- [[Agent Harness]]
- [[Orchestration Loop]]
