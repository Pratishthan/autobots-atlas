---
tags: [ai-agents, llm-tooling, orchestration, ai-sdlc]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Agent Harness

The complete software infrastructure wrapping an LLM: [[Orchestration Loop]], tools, [[Agent Memory]], [[Context Management]], state persistence, error handling, and guardrails. The term was formalized in early 2026, though the concept existed before.

> **"If you're not the model, you're the harness."** — [[Vivek Trivedy]], [[LangChain]]

The "agent" is the emergent behavior: the goal-directed, tool-using, self-correcting entity the user interacts with. The harness is the machinery producing that behavior. When someone says "I built an agent," they mean they built a harness and pointed it at a model.

## Computer Architecture Analogy

[[Beren Millidge]] (2023): a raw LLM is a CPU with no RAM, no disk, and no I/O.

| Harness Component | Computer Analogue |
|---|---|
| Context window | RAM (fast, limited) |
| External databases | Disk storage (large, slow) |
| Tool integrations | Device drivers |
| The harness | Operating system |

"We have reinvented the Von Neumann architecture."

## The 12 Components

A production agent harness has twelve distinct components (synthesized from [[Anthropic]], [[OpenAI]], [[LangChain]], and the broader practitioner community):

1. **[[Orchestration Loop]]** — the TAO/[[ReAct Loop]] cycle; runs "assemble prompt → call LLM → parse output → execute tools → feed results back → repeat"
2. **Tools** — registered as schemas (name, description, parameter types); layer handles registration, validation, execution, result capture, formatting
3. **[[Agent Memory]]** — short-term (session), long-term (persistent); multi-timescale architecture
4. **[[Context Management]]** — preventing [[Context Rot]]; compaction, masking, just-in-time retrieval, sub-agent delegation
5. **Prompt Construction** — hierarchical assembly: system prompt → tool definitions → memory files → conversation history → current message
6. **Output Parsing** — modern harnesses use native tool calling (structured `tool_calls` objects); schema-constrained responses via Pydantic for structured output
7. **State Management** — LangGraph: typed dict state with reducers; OpenAI: four strategies (app memory, SDK sessions, Conversations API, `previous_response_id`); [[Claude Code]]: git commits + progress files
8. **Error Handling** — LangGraph's four error types: transient (retry), LLM-recoverable (return as ToolMessage), user-fixable (interrupt), unexpected (bubble up). A 10-step process at 99% per-step success = ~90.4% end-to-end success.
9. **Guardrails and Safety** — input/output/tool-level guardrails; tripwire mechanisms; architectural separation of model intent from tool permissions
10. **[[Verification Loops]]** — rules-based (tests/linters), visual (screenshots), LLM-as-judge; improves quality 2-3x ([[Boris Cherny]])
11. **[[Subagent Orchestration]]** — Fork, Teammate, Worktree; handoffs; nested state graphs; agents-as-tools

## [[Three Levels of Engineering]]

- **Prompt engineering** — crafts instructions the model receives
- **Context engineering** — manages what the model sees and when
- **Harness engineering** — encompasses both, plus the full application infrastructure

## [[Harness Thickness]]

The core architectural bet: how much logic lives in the harness vs. the model. [[Anthropic]] bets on thin harnesses. Graph-based frameworks ([[LangChain]]/LangGraph) bet on explicit control. The trend is toward thinner harnesses as model capability grows ([[Co-evolution Principle]]).

## Seven Architectural Decisions

Every harness architect must choose:

1. **Single-agent vs. multi-agent** — both [[Anthropic]] and [[OpenAI]] say maximize a single agent first; split only when >~10 overlapping tools or clearly separate domains
2. **[[ReAct Loop]] vs. plan-and-execute** — ReAct is flexible but higher per-step cost; LLMCompiler reports 3.6x speedup over sequential ReAct
3. **Context window strategy** — five approaches: time-based clearing, summarization, observation masking, structured note-taking, sub-agent delegation; ACON research shows 26–54% token reduction while preserving 95%+ accuracy
4. **[[Verification Loops]] design** — computational (deterministic ground truth) vs. inferential (LLM-as-judge); guides (feedforward) vs. sensors (feedback) framing from Martin Fowler/Thoughtworks
5. **Permission and safety architecture** — permissive (fast, risky) vs. restrictive (safe, slow)
6. **[[Tool Scoping]]** — Vercel removed 80% of tools from v0 and got better results; [[Claude Code]] achieves 95% context reduction via lazy loading
7. **[[Harness Thickness]]** — thin harness (bet on model) vs. thick harness (explicit control)

## Evidence That Harnesses Matter

- [[LangChain]]: same model, changed only harness → moved from outside top 30 to rank 5 on [[TerminalBench]] 2.0
- Research project: LLM optimizing its own infrastructure → 76.4% pass rate, surpassing hand-designed systems
- [[Manus]]: rebuilt 5 times in 6 months, each rewrite removing complexity as the model improved

## Related

- [[Orchestration Loop]]
- [[Context Management]]
- [[Agent Memory]]
- [[Verification Loops]]
- [[Subagent Orchestration]]
- [[ReAct Loop]]
- [[Harness Thickness]]
- [[Co-evolution Principle]]
- [[Three Levels of Engineering]]
- [[Tool Scoping]]
- [[Context Rot]]
- [[Ralph Loop Pattern]]
