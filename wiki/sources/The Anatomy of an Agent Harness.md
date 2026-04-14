---
tags: [ai-agents, agent-harness, llm-tooling, orchestration, context-management, ai-sdlc]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# The Anatomy of an Agent Harness

**Source:** The Anatomy of an Agent Harness.md
**Original URL:** https://x.com/akshay_pachaar/status/2041146899319971922
**Author:** [[Akshay Pachaar]]
**Published:** 2026-04-06
**Date ingested:** 2026-04-13
**Type:** article (Twitter/X thread)

## Summary

A deep dive into what [[Anthropic]], [[OpenAI]], [[LangChain]], and others are actually building when they build agents. The article formalizes the concept of the [[Agent Harness]] — the complete software infrastructure wrapping an LLM — and enumerates its 12 components, compares implementations across major frameworks, and outlines 7 key architectural decisions every harness builder must make.

## Key Claims

- The term "agent harness" was formalized in early 2026, but the concept existed before.
- [[LangChain]] jumped from outside the top 30 to rank 5 on [[TerminalBench]] 2.0 by changing only the harness infrastructure around the same model.
- A research project achieved 76.4% pass rate by having an LLM optimize the infrastructure itself, surpassing hand-designed systems.
- [[Beren Millidge]]'s 2023 essay frames the harness as an OS: context window = RAM, external databases = disk, tool integrations = device drivers, harness = operating system.
- [[Vivek Trivedy]] (LangChain): "If you're not the model, you're the harness."
- Model performance degrades 30%+ when key content falls in mid-window positions (context rot).
- Giving the model a way to verify its work improves quality 2-3x ([[Boris Cherny]], creator of [[Claude Code]]).
- [[Manus]] was rebuilt 5 times in 6 months, each rewrite removing harness complexity as models improved.
- The trend is toward thinner harnesses as model capability grows ([[Co-evolution Principle]]).

## Entities Mentioned

- [[Akshay Pachaar]] — author of the article
- [[Anthropic]] — Claude Code, Claude Agent SDK
- [[OpenAI]] — Agents SDK, Codex
- [[LangChain]] — LangGraph, Deep Agents, AgentExecutor
- [[CrewAI]] — role-based multi-agent framework
- [[AutoGen]] — conversation-driven orchestration (evolving into Microsoft Agent Framework)
- [[Claude Code]] — Anthropic's coding agent; used as primary reference implementation
- [[Boris Cherny]] — creator of Claude Code
- [[Beren Millidge]] — author of "Scaffolded LLMs as Natural Language Computers" (2023)
- [[Vivek Trivedy]] — LangChain; coined "If you're not the model, you're the harness"
- [[Manus]] — AI agent rebuilt 5 times, illustrating co-evolution principle
- [[TerminalBench]] — benchmark used to measure harness impact

## Concepts Covered

- [[Agent Harness]] — the complete infrastructure wrapping an LLM
- [[Orchestration Loop]] — the TAO/ReAct cycle driving agent execution
- [[Three Levels of Engineering]] — prompt engineering, context engineering, harness engineering
- [[Context Management]] — strategies for preventing context rot
- [[Agent Memory]] — multi-timescale memory architecture
- [[Verification Loops]] — rules-based, visual, and LLM-as-judge feedback
- [[Subagent Orchestration]] — Fork, Teammate, Worktree, handoff, nested graph patterns
- [[ReAct Loop]] — Thought-Action-Observation cycle
- [[Harness Thickness]] — how much logic lives in harness vs. model
- [[Co-evolution Principle]] — models post-trained with specific harnesses; tight coupling between model and harness
- [[Ralph Loop Pattern]] — two-phase pattern for long-running tasks spanning multiple context windows
- [[Tool Scoping]] — exposing minimum tool set for current step
- [[Context Rot]] — degradation when key content falls in mid-window positions
