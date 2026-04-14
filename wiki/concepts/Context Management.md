---
tags: [ai-agents, context-management, llm-tooling]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Context Management

One of the 12 components of the [[Agent Harness]], and where many agents fail silently. The core problem is [[Context Rot]].

> The goal: find the **smallest possible set of high-signal tokens** that maximize likelihood of the desired outcome. — [[Anthropic]] context engineering guide

## The Problem

- Model performance degrades **30%+** when key content falls in mid-window positions (Chroma research, corroborated by Stanford's "Lost in the Middle" finding)
- Even million-token context windows suffer instruction-following degradation as context grows
- Context windows fill up with low-signal content (redundant tool outputs, intermediate steps)

## Production Strategies

### 1. Compaction / Summarization
Summarize conversation history when approaching context limits. [[Claude Code]] preserves:
- Architectural decisions
- Unresolved bugs
While discarding: redundant tool outputs.

### 2. Observation Masking
Hide old tool outputs while keeping tool calls visible. Used by JetBrains' Junie.

### 3. Just-in-Time Retrieval
Maintain lightweight identifiers; load data dynamically only when needed. [[Claude Code]] uses grep, glob, head, tail rather than loading full files. Achieves ~95% context reduction via lazy loading.

### 4. Sub-agent Delegation
Each subagent explores extensively but returns only 1,000–2,000 token condensed summaries to the parent agent.

### 5. Structured Note-Taking
Maintain structured progress files that capture key state rather than relying on raw conversation history.

## Prompt Positioning

Counter the "Lost in the Middle" effect by placing important context at the **beginning and end** of the prompt, not the middle.

## Research Results

- ACON research: 26–54% token reduction while preserving 95%+ accuracy by prioritizing reasoning traces over raw tool outputs.

## [[Three Levels of Engineering]] Connection

Context management sits at the intersection of context engineering (what the model sees) and harness engineering (the infrastructure that manages it). It's distinct from prompt engineering (crafting instructions).

## Related

- [[Context Rot]]
- [[Agent Harness]]
- [[Orchestration Loop]]
- [[Agent Memory]]
- [[Subagent Orchestration]]
- [[Three Levels of Engineering]]
- [[Claude Code]]
