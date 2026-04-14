# Index

Master catalog of all wiki pages. Updated on every ingest.

## Sources

- [[The Anatomy of an Agent Harness]] — April 2026 article synthesizing agent harness design across Anthropic, OpenAI, LangChain, CrewAI, AutoGen
- [[Build Agents That Never Forget]] — April 2026 walk through agent memory: list → markdown → vector → graph-vector hybrid

## Entities

- [[Akshay Pachaar]] — AI/ML educator; author of "The Anatomy of an Agent Harness"
- [[Anthropic]] — AI safety company; Claude models, Claude Code, Claude Agent SDK
- [[AutoGen]] — Microsoft's conversation-driven multi-agent framework (→ Microsoft Agent Framework)
- [[Beren Millidge]] — researcher; "Scaffolded LLMs as Natural Language Computers" (2023)
- [[Boris Cherny]] — creator of Claude Code at Anthropic
- [[Claude Code]] — Anthropic's coding agent; primary reference implementation for harness design
- [[Cognee]] — open-source knowledge engine; relational + vector + graph stores for agent memory
- [[CrewAI]] — role-based multi-agent framework with deterministic Flows layer
- [[LangChain]] — AI tooling company; LangChain framework, LangGraph, Deep Agents
- [[Lilian Weng]] — researcher; "Agent = LLM + Memory + Planning + Tool Use" framing
- [[Manus]] — AI agent rebuilt 5× in 6 months; illustrates co-evolution principle
- [[OpenAI]] — AI company; GPT models, Agents SDK, Codex
- [[TerminalBench]] — benchmark for coding agents; LangChain used it to prove harness impact
- [[Vivek Trivedy]] — LangChain; coined "If you're not the model, you're the harness"

## Concepts

- [[Agent Harness]] — complete software infrastructure wrapping an LLM; the central concept
- [[Agent Memory]] — multi-timescale memory architecture (short-term, long-term, three-tier)
- [[Agent Memory Layers]] — evolutionary ladder: list → markdown → vector → graph+vector
- [[Co-evolution Principle]] — models are post-trained with specific harnesses; tight coupling
- [[Context Management]] — strategies to prevent context rot and keep context high-signal
- [[Context Rot]] — 30%+ performance degradation from mid-window content placement
- [[Dual Index Retrieval]] — hybrid graph+vector retrieval; every node has an embedding
- [[Episodic Memory]] — specific past events; raw material for memory consolidation
- [[Harness Thickness]] — how much logic lives in harness vs. model; thin vs. thick spectrum
- [[Knowledge Graph for Agent Memory]] — nodes/edges as the relational layer of agent memory
- [[Lost in the Middle]] — 30%+ accuracy drop on mid-window content, even in 128K+ windows
- [[Memory Consolidation]] — episodic events distilled into semantic/procedural knowledge
- [[Orchestration Loop]] — the TAO/ReAct cycle; heartbeat of the agent harness
- [[Procedural Memory]] — skills and workflows; action-shaped long-term knowledge
- [[Ralph Loop Pattern]] — two-phase pattern for long-running tasks spanning multiple context windows
- [[ReAct Loop]] — Thought-Action-Observation cycle; core of the orchestration loop
- [[Semantic Memory]] — general facts and concepts, stripped of episodic context
- [[Subagent Orchestration]] — patterns for spawning and coordinating multiple agents
- [[Three Levels of Engineering]] — prompt, context, and harness engineering (innermost to outermost)
- [[Tool Scoping]] — expose minimum tool set per step; more tools often means worse performance
- [[Verification Loops]] — rules-based, visual, LLM-as-judge feedback; improves quality 2-3x

## Synthesis
