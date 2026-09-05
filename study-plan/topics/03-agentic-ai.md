# Topic 3: Agentic AI & Multi-Agent Systems

## Core Concepts

### Agent Fundamentals
- **Agent loop:** perceive (context) → think (LLM) → act (tool call) → observe (result) → repeat
- **ReAct pattern:** interleave reasoning traces with action calls — gives the model room to think
- **Tool design:** clear schema + description is half the battle; bad tool descriptions = bad agent
- **Memory types:**
  - In-context: everything in the current prompt window
  - External: vector DB for episodic memory or knowledge retrieval
  - Procedural: system prompt with persistent rules/persona
- **Termination:** max iterations, stop token, explicit "task complete" tool call
- **Failure modes:** loops, hallucinated tool calls, cascading errors — design for recovery

### Multi-Agent Systems
- **Supervisor architecture:** one orchestrator routes subtasks to specialized worker agents
- **Peer-to-peer:** agents communicate directly — harder to debug, use sparingly
- **State passing:** each agent sees only what it needs (minimize context bloat)
- **Parallelization:** independent subtasks can run concurrently — big latency win
- **Human-in-the-loop:** explicit approval nodes for high-stakes actions

### Model Context Protocol (MCP)
- **What it is:** standard protocol for LLMs to discover and call external tools/resources
- **Architecture:** MCP server exposes tools + resources; client (Claude, any agent) connects
- **Why it matters:** write once, works with any MCP-compatible AI client; emerging standard

## The One Resource

**DeepLearning.AI — [AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/)** (free, 5hr)  
Best practical intro to building real agents. Covers LangGraph, tool use, memory, and multi-agent.

**Essential read:** [Anthropic — Building Effective Agents](https://www.anthropic.com/research/building-effective-agents)  
The clearest engineering-focused guide on when and how to build agents. Required reading.

**For MCP:** [modelcontextprotocol.io](https://modelcontextprotocol.io/introduction) — official spec + quickstart

## Must-Read Papers

- [ReAct: Synergizing Reasoning and Acting](https://arxiv.org/abs/2210.03629) — foundational agent pattern
- [AutoGen](https://arxiv.org/abs/2308.08155) — multi-agent framework paper (read intro + architecture)

## Key Libraries

| Library | Use |
|---------|-----|
| `langgraph` | Graph-based agent orchestration (preferred) |
| `langsmith` | Agent tracing + observability |
| `tavily-python` | Web search tool for agents |
| `mcp` | MCP Python SDK for building servers |
| `anthropic` | Direct API — ReAct agents without frameworks |

## Projects

- **P3 — Multi-Agent Research Pipeline** — see [week-by-week.md](../week-by-week.md) weeks 9–11
- **MCP Server** — week 12 — wrap a real API, publish to GitHub

## Interview Questions

1. Describe the ReAct pattern. Why does interleaving reasoning help?
2. How do you prevent an agent from looping indefinitely?
3. When would you use a supervisor pattern vs peer-to-peer agents?
4. How do agents handle memory across long task horizons?
5. What is MCP and how is it different from function calling?
6. How would you design a customer support agent with safe fallback to a human?
7. How do you evaluate an agentic system? What metrics matter?
8. What are the biggest safety risks in agentic systems and how do you mitigate them?
