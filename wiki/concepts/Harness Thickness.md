---
tags: [ai-agents, llm-tooling, software-engineering]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Harness Thickness

The architectural decision of how much logic lives in the [[Agent Harness]] versus in the model itself. One of the seven key decisions every harness architect faces.

## The Spectrum

**Thin harness** (bet on the model):
- Minimal orchestration logic in code
- Model handles planning, routing, and decision-making
- Harness just manages turns and tool execution
- [[Anthropic]]'s philosophy: regularly delete planning steps from [[Claude Code]]'s harness as new model versions internalize capabilities

**Thick harness** (explicit control):
- Significant orchestration logic in code (state graphs, explicit routing, planning steps)
- More deterministic and debuggable
- [[LangChain]]/LangGraph approach: explicit state graphs with typed reducers

## The Trend

The field is moving toward **thinner harnesses** as models improve. [[Manus]] was rebuilt 5 times, each rewrite removing complexity. The [[Co-evolution Principle]] explains why: models are now post-trained with specific harnesses, internalizing behaviors that previously required explicit harness logic.

## The "Future-Proofing Test"

If performance scales up with more powerful models **without adding harness complexity**, the design is sound.

## The Scaffolding Metaphor

Construction scaffolding is temporary infrastructure that enables workers to build a structure they couldn't reach otherwise. It doesn't do the construction — but without it, workers can't reach the upper floors.

Key insight: **scaffolding is removed when the building is complete.** As models improve, harness scaffolding should decrease.

## Related

- [[Agent Harness]]
- [[Co-evolution Principle]]
- [[Manus]]
- [[Anthropic]]
- [[LangChain]]
