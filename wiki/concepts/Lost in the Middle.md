---
tags: [llm, context-management, research]
sources: [Build Agents that never forget.md, The Anatomy of an Agent Harness.md]
created: 2026-04-14
updated: 2026-04-14
---

# Lost in the Middle

A well-documented failure mode of large context windows: **accuracy drops over 30% when relevant information sits in the middle of a long context**, even when the window is nominally large enough to fit everything.

LLMs attend more strongly to content at the beginning and end of a prompt. Information in the middle is systematically under-attended, regardless of the headline token limit.

## Implications

- Expanding to 128K or 200K windows does not, by itself, solve memory or retrieval. See [[Agent Memory Layers]].
- Context is a **shared budget** — system prompt, retrieved docs, conversation history, and output all compete for the same tokens. Absence of persistence, prioritization, and salience makes raw length insufficient.
- Motivates the active-management strategies catalogued in [[Context Management]] and makes [[Context Rot]] a first-class design concern.

## Related

- [[Context Rot]]
- [[Context Management]]
- [[Agent Memory]]
