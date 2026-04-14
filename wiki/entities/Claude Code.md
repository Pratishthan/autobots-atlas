---
tags: [product, ai-agents, llm-tooling, code-generation, ai-sdlc]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Claude Code

[[Anthropic]]'s coding agent. Created by [[Boris Cherny]]. Serves as the primary reference implementation for [[Anthropic]]'s [[Agent Harness]] design philosophy.

## Harness Architecture

Claude Code operates on a **Gather-Act-Verify** cycle:
1. **Gather** — search files, read code (grep, glob, head, tail — never loading full files)
2. **Act** — edit files, run commands
3. **Verify** — run tests, check output
4. Repeat

The runtime is a "dumb loop." All intelligence lives in the model.

## Memory System

Three-tier hierarchy:
- **Tier 1**: Lightweight index (~150 chars/entry) — always loaded into context
- **Tier 2**: Detailed topic files — pulled in on demand
- **Tier 3**: Raw transcripts — accessed via search only

Design principle: the agent treats its own memory as a "hint" and verifies against actual state before acting. See [[Agent Memory]].

## Context Management

- Just-in-time retrieval: uses grep/glob/head/tail rather than loading full files
- Sub-agents return only 1,000–2,000 token condensed summaries
- Compaction: preserves architectural decisions and unresolved bugs; discards redundant tool outputs
- Achieves ~95% context reduction via lazy loading

See [[Context Management]].

## State Management

- Git commits as checkpoints
- Progress files as structured scratchpads
- For long-running tasks: [[Ralph Loop Pattern]] — Initializer Agent sets up environment, Coding Agent reads git logs + progress files to orient each session

## Safety and Permissions

- ~40 discrete tool capabilities gated independently
- Three stages: trust establishment at project load → permission check before each tool call → explicit user confirmation for high-risk operations
- Architectural separation: model decides what to attempt; tool system decides what's allowed

## Tools

Six categories: file operations, search, execution, web access, code intelligence, and subagent spawning.

## Subagent Execution Models

Three modes for spawning subagents:
- **Fork** — byte-identical copy of parent context
- **Teammate** — separate terminal pane with file-based mailbox communication
- **Worktree** — own git worktree, isolated branch per agent

## SDK

The Claude Agent SDK powers Claude Code. Exposed as a `query()` function returning an async iterator streaming messages.

## Verification

Giving the model a way to verify its work improves quality **2-3x** (Boris Cherny).

Three verification approaches:
- Rules-based: tests, linters, type checkers
- Visual: screenshots via Playwright
- LLM-as-judge: separate subagent evaluates output

## Related

- [[Anthropic]]
- [[Boris Cherny]]
- [[Agent Harness]]
- [[Ralph Loop Pattern]]
- [[Verification Loops]]
- [[Context Management]]
- [[Agent Memory]]
- [[Co-evolution Principle]]
