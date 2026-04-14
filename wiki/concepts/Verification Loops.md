---
tags: [ai-agents, verification, software-engineering, ai-sdlc]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Verification Loops

One of the 12 components of the [[Agent Harness]]. What separates toy demos from production agents.

> Giving the model a way to verify its work improves quality by **2-3x**. — [[Boris Cherny]], creator of [[Claude Code]]

## Three Approaches

### 1. Rules-Based (Computational)
Tests, linters, type checkers. Provides **deterministic ground truth**. Fast and reliable.

### 2. Visual Feedback
Screenshots via Playwright for UI tasks. Allows the agent to see what the user would see.

### 3. LLM-as-Judge (Inferential)
A separate subagent evaluates output. Catches **semantic issues** that tests can't — logic errors, wrong behavior that passes syntactically. Adds latency.

## Guides vs. Sensors

Martin Fowler's Thoughtworks team framing:
- **Guides** (feedforward) — steer before action; prevent errors
- **Sensors** (feedback) — observe after action; correct errors

Both types belong in a production harness.

## Error Compounding

Without verification loops, errors compound rapidly. A 10-step process with 99% per-step success rate has only **~90.4% end-to-end success**. Verification loops catch and correct errors before they propagate.

## Recommendations

[[Anthropic]] recommends all three approaches for production harnesses. The combination gives both deterministic correctness and semantic correctness.

## Related

- [[Agent Harness]]
- [[Boris Cherny]]
- [[Claude Code]]
- [[Subagent Orchestration]]
