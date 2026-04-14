---
tags: [ai-agents, orchestration, ai-sdlc, patterns]
sources: [The Anatomy of an Agent Harness.md]
created: 2026-04-13
updated: 2026-04-13
---

# Ralph Loop Pattern

A two-phase pattern developed by [[Anthropic]] for long-running agent tasks that span multiple context windows. Solves the problem of maintaining continuity when no single context window can hold an entire task.

## The Two Phases

### Phase 1: Initializer Agent
Runs once at the start of the task:
- Sets up environment
- Creates init script
- Creates progress file (structured scratchpad)
- Creates feature list
- Makes initial git commit

### Phase 2: Coding Agent (repeated sessions)
In every subsequent session:
1. Reads git logs to understand what has been done
2. Reads progress files to understand current state
3. Picks the highest-priority incomplete feature
4. Works on it
5. Commits changes
6. Writes summary to progress file
7. Session ends (context window exhausted or task complete)
8. Next session starts at step 1

## Key Insight

**The filesystem provides continuity across context windows.** Git commits and progress files replace the context window as the source of state — the agent doesn't need to remember; it reads.

## Related

- [[Agent Harness]]
- [[Orchestration Loop]]
- [[Agent Memory]]
- [[Claude Code]]
- [[Anthropic]]
