# Agents and Tool-Using Systems

## TL;DR
An "agent" in the LLM world is an LLM-centric system that can plan and execute actions using tools (APIs, search, code, databases) to achieve a goal, often with memory and feedback loops.

## Intuition
- The LLM is the "brain" that decides what to do next.
- Tools extend the LLM beyond text-only reasoning into actions and retrieval.
- A good agent system balances autonomy with safety and control.

## Core Concepts
- Tool/function calling.
- Planner vs executor roles.
- Memory (short-term vs long-term).
- Single-agent vs multi-agent setups.

## Simple Example
- User asks: "Summarize recent news on RAG and send me key points."
- Agent:
  - Uses a search tool to find articles.
  - Uses RAG over results.
  - Calls another tool (email/notification) to send a summary.

## Gotchas & Common Pitfalls
- Infinite loops or unnecessary tool calls.
- Unsafe or expensive actions.
- Debugging and observability challenges.

## Connections
- Related topics:
  - [[llm-basics]]
  - [[rag]]
- Related projects:
  - [[mini-rag-bot]]

## References / Resources
- Paper / blog:
- Notes:
