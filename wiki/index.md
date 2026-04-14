# Index

Master catalog of all wiki pages. Updated on every ingest.

## Sources

- [[The Anatomy of an Agent Harness]] — April 2026 article synthesizing agent harness design across Anthropic, OpenAI, LangChain, CrewAI, AutoGen

## Entities

- [[Akshay Pachaar]] — AI/ML educator; author of "The Anatomy of an Agent Harness"
- [[Anthropic]] — AI safety company; Claude models, Claude Code, Claude Agent SDK
- [[AutoGen]] — Microsoft's conversation-driven multi-agent framework (→ Microsoft Agent Framework)
- [[Beren Millidge]] — researcher; "Scaffolded LLMs as Natural Language Computers" (2023)
- [[Boris Cherny]] — creator of Claude Code at Anthropic
- [[Claude Code]] — Anthropic's coding agent; primary reference implementation for harness design
- [[CrewAI]] — role-based multi-agent framework with deterministic Flows layer
- [[LangChain]] — AI tooling company; LangChain framework, LangGraph, Deep Agents
- [[Manus]] — AI agent rebuilt 5× in 6 months; illustrates co-evolution principle
- [[OpenAI]] — AI company; GPT models, Agents SDK, Codex
- [[TerminalBench]] — benchmark for coding agents; LangChain used it to prove harness impact
- [[Vivek Trivedy]] — LangChain; coined "If you're not the model, you're the harness"

## Concepts

- [[Agent Harness]] — complete software infrastructure wrapping an LLM; the central concept
- [[Agent Memory]] — multi-timescale memory architecture (short-term, long-term, three-tier)
- [[Co-evolution Principle]] — models are post-trained with specific harnesses; tight coupling
- [[Context Management]] — strategies to prevent context rot and keep context high-signal
- [[Context Rot]] — 30%+ performance degradation from mid-window content placement
- [[Harness Thickness]] — how much logic lives in harness vs. model; thin vs. thick spectrum
- [[Orchestration Loop]] — the TAO/ReAct cycle; heartbeat of the agent harness
- [[Ralph Loop Pattern]] — two-phase pattern for long-running tasks spanning multiple context windows
- [[ReAct Loop]] — Thought-Action-Observation cycle; core of the orchestration loop
- [[Subagent Orchestration]] — patterns for spawning and coordinating multiple agents
- [[Three Levels of Engineering]] — prompt, context, and harness engineering (innermost to outermost)
- [[Tool Scoping]] — expose minimum tool set per step; more tools often means worse performance
- [[Verification Loops]] — rules-based, visual, LLM-as-judge feedback; improves quality 2-3x

## Synthesis
