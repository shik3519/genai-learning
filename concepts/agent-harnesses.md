# Agent Harnesses: Why the Harness Matters More Than the Model

## One-line summary
The same model weights can swing from 30% to 95%+ on a hard benchmark (ARC-AGI) purely based on the harness wrapped around them — the loop, context assembly, tool/skill access, and sub-agent orchestration. Harness engineering is real engineering, not "just scaffolding."

## How it works
A **harness** is everything between the raw model weights and the world: the agentic loop (plan → act → observe → repeat), how context gets assembled and managed, what tools/skills the model can reach for, whether/how it can spawn sub-agents, and — increasingly — the harness's own code becoming something the agent can inspect or modify.

The headline evidence from YC Paper Club (Sept 2026): **Prime Agent** (Prime Intellect, presented by Seth Karten) is a self-improving harness that raised ARC-AGI-3 performance from 30% to 95.5% on the *same underlying model* — exceeding the reported human-expert baseline. The model didn't get smarter; the harness around it did.

Two other examples from the same session:
- **QM** (Josh France & Regan Bell) — the multi-agent harness YC built for its own internal staff, running 50+ individual agents across accounting, legal, events, and engineering. Open-sourced under MIT (July 2026).
- **OpenJarvis** — personal/local AI, focused on cost efficiency and optimization strategies for running agents on-device.

## Intuition / mental model
Model weights are the engine; the harness is the car built around it — transmission, steering, sensors, the driver's actual skill at using all of it. A better driver in a worse car can beat a mediocre driver in a great engine. This directly explains why "prompt engineering" and "agent scaffolding" get dismissed as unserious compared to model training, when the ARC-AGI evidence says the opposite: the harness can be the dominant factor.

## When it's used
- **This is the theoretical anchor for the whole Agentic Coding track** (`study-plan/tracks/agentic-coding.md`) — the reason deliberately getting good at harness usage (Claude Code workflows, custom commands, subagents, MCP) is a real skill investment, not just convenience. If harness quality can be a 3x performance multiplier on the *same* model, then how well you use/configure your harness is directly comparable in leverage to model choice.
- Worth revisiting when evaluating any agentic system (including your own P3 multi-agent pipeline) — the question "is this a model problem or a harness problem?" is often more actionable than it first appears.

## Related
- [[instruction-based-retrievers]] — a different domain, same pattern: how a model is *used* (instructions, reasoning traces) can matter as much as its base training
- Source: [Why The Harness Matters More Than The Model | YC Paper Club](https://youtu.be/n9xKblqyQ28) (Sept 2026)
