---
tags: [organization, ai-agents, llm-tooling, ai-sdlc]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Anthropic

AI safety company and creator of the Claude family of models. In the agent infrastructure space, Anthropic ships [[Claude Code]] (a coding agent) and the Claude Agent SDK.

## Agent SDK

The Claude Agent SDK exposes the [[Agent Harness]] through a single `query()` function that creates the agentic loop and returns an async iterator streaming messages. The runtime is described as a "dumb loop" — all intelligence lives in the model; the harness just manages turns.

## Claude Code Harness Design

[[Claude Code]] implements a Gather-Act-Verify cycle:
1. **Gather** — search files, read code
2. **Act** — edit files, run commands
3. **Verify** — run tests, check output, repeat

Key design choices in Claude Code's harness:
- **Memory**: Three-tier hierarchy — lightweight index (~150 chars/entry, always loaded), detailed topic files pulled on demand, raw transcripts via search only. The agent treats its own memory as a "hint" and verifies against actual state before acting.
- **Context**: Just-in-time retrieval via grep/glob/head/tail rather than loading full files; sub-agents return only 1,000–2,000 token condensed summaries.
- **State**: Git commits as checkpoints, progress files as structured scratchpads.
- **Safety**: ~40 discrete tool capabilities gated independently — trust establishment at project load, permission check before each tool call, explicit confirmation for high-risk operations. Model decides what to attempt; tool system decides what's allowed (architectural separation).
- **Verification**: Tests, linters, type checkers (rules-based); screenshots via Playwright (visual); LLM-as-judge subagent (inferential).

## Context Engineering Guidance

Anthropic's context engineering guide states the goal: find the **smallest possible set of high-signal tokens** that maximize likelihood of the desired outcome.

## Harness Philosophy

Anthropic bets on **thin harnesses** and model improvement. They regularly delete planning steps from Claude Code's harness as new model versions internalize that capability. The model is post-trained with the specific harness it operates in ([[Co-evolution Principle]]).

## Related

- [[Claude Code]]
- [[Agent Harness]]
- [[Boris Cherny]]
- [[Co-evolution Principle]]
- [[Context Management]]
- [[Harness Thickness]]
