---
tags: [ai-agents, orchestration, llm-tooling]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Orchestration Loop

The heartbeat of the [[Agent Harness]]. Implements the Thought-Action-Observation (TAO) cycle, also called the [[ReAct Loop]].

## Mechanics

The loop runs:
1. Assemble prompt
2. Call LLM
3. Parse output
4. Execute any tool calls
5. Feed results back
6. Repeat until done

Mechanically, it's often just a `while` loop. **The complexity lives in everything the loop manages**, not the loop itself. [[Anthropic]] describes their runtime as a "dumb loop" — all intelligence lives in the model; the harness just manages turns.

## Step-by-Step Walkthrough

**Step 1 (Prompt Assembly):** System prompt + tool schemas + memory files + conversation history + current user message. Important context is positioned at the beginning and end (addressing the "Lost in the Middle" [[Context Rot]] problem).

**Step 2 (LLM Inference):** Assembled prompt goes to the model API. Output: text, tool call requests, or both.

**Step 3 (Output Classification):** 
- Text with no tool calls → loop ends
- Tool calls requested → proceed to execution
- Handoff requested → update current agent, restart

**Step 4 (Tool Execution):** Validate arguments, check permissions, execute in sandboxed environment, capture results. Read-only operations can run concurrently; mutating operations run serially.

**Step 5 (Result Packaging):** Format tool results as LLM-readable messages. Errors returned as error results so the model can self-correct.

**Step 6 (Context Update):** Append results to conversation history. If approaching context window limit, trigger compaction.

**Step 7 (Loop):** Return to Step 1.

## Termination Conditions

- Model produces response with no tool calls
- Maximum turn limit exceeded
- Token budget exhausted
- Guardrail tripwire fires
- User interrupts
- Safety refusal returned

A simple question: 1–2 turns. A complex refactoring task: dozens of tool calls across many turns.

## Framework Implementations

- **[[Anthropic]] Claude Agent SDK**: `query()` function returns async iterator; runtime is a "dumb loop"
- **[[OpenAI]] Agents SDK**: `Runner` class with async/sync/streamed modes
- **LangGraph ([[LangChain]])**: explicit state graph — two nodes (`llm_call`, `tool_node`) with conditional routing

## Related

- [[Agent Harness]]
- [[ReAct Loop]]
- [[Context Management]]
- [[Tool Scoping]]
