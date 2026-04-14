---
tags: [ai-agents, llm-tooling, software-engineering]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Co-evolution Principle

Models are now post-trained with specific [[Agent Harness|harnesses]] in the training loop. This creates tight coupling between a model's behavior and the harness it was trained with.

## Implications

1. **Changing tool implementations can degrade performance** — because the model's behavior was shaped by the specific tool schemas and harness design it was trained with.
2. **Harnesses evolve alongside models** — as models become more capable, harness complexity should decrease. Behaviors that required explicit harness logic get internalized into the model.
3. **You can't freely swap harnesses** — a model trained with Harness A may underperform when wrapped with Harness B, even if B is technically superior by other metrics.

## Empirical Evidence

- [[Claude Code]]'s model learned to use the specific harness it was trained with. [[Anthropic]] regularly deletes planning steps from the harness as new model versions internalize that capability.
- [[Manus]] was rebuilt 5 times in 6 months, each rewrite removing harness complexity as the underlying model improved.

## Design Implication

The [[Harness Thickness|future-proofing test]]: if performance scales up with more powerful models without adding harness complexity, the design is sound. This suggests designing for model capability growth from the start.

## Related

- [[Agent Harness]]
- [[Harness Thickness]]
- [[Claude Code]]
- [[Manus]]
- [[Anthropic]]
