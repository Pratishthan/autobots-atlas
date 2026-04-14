---
tags: [ai-agents, software-engineering, prompt-engineering, context-management]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Three Levels of Engineering

Three concentric levels of engineering surround an LLM in a production agent system, from innermost to outermost:

## Level 1: Prompt Engineering
Crafts the **instructions** the model receives. What to do, how to behave, what persona to take. The most familiar and most discussed level.

## Level 2: Context Engineering
Manages **what the model sees and when** — which information is in the context window at each step. Includes retrieval, compaction, ordering, and filtering. See [[Context Management]].

## Level 3: Harness Engineering
Encompasses levels 1 and 2, plus the **complete application infrastructure**: tool orchestration, state persistence, error recovery, [[Verification Loops]], safety enforcement, and lifecycle management. See [[Agent Harness]].

## Key Distinction

The harness is not a wrapper around a prompt. It is the complete system that makes autonomous agent behavior possible.

Most public discourse focuses on Level 1 (prompt engineering). Most of the real performance work happens at Levels 2 and 3.

## Related

- [[Agent Harness]]
- [[Context Management]]
- [[Context Rot]]
