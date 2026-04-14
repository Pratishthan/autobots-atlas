---
tags: [ai-agents, llm-tooling, software-engineering]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Tool Scoping

The practice of exposing only the minimum tool set needed for the current step. One of the seven key architectural decisions in [[Agent Harness]] design.

## The Counter-Intuitive Finding

More tools often means **worse performance**. Reasons:
- Tool definitions consume context tokens
- More choices increase decision complexity for the model
- Irrelevant tools introduce noise into model reasoning

## Evidence

- Vercel removed **80% of tools** from v0 and got better results
- [[Claude Code]] achieves **95% context reduction** via lazy loading — tools and files are loaded on demand, not upfront

## The Principle

> Expose the minimum tool set needed for the current step.

This can be implemented via:
- **Lazy loading** — load tool schemas only when the agent enters a context where they're relevant
- **Dynamic tool registration** — register/unregister tools as task phase changes
- **Sub-agent specialization** — give each sub-agent only the tools relevant to its role

## Related

- [[Agent Harness]]
- [[Context Management]]
- [[Subagent Orchestration]]
- [[Claude Code]]
