# GenAI Study Plan — Interview Ready + Paper Submitted by Early 2027

**Target:** Applied Scientist at Apple, Netflix, Google, Meta, Anthropic
**Timeline:** 19 weeks (September 2026 → ~mid-January 2027), flex as needed
**Starting point:** AS3 with production LLM experience on Bedrock. Concepts familiar but not interview-deep. Open-source stack (HuggingFace, LangGraph, vLLM, PEFT) is largely new. Currently working a retrieval-systems project at Amazon.

**Compute:** access to larger internal Amazon compute for small-scale projects — use it to go beyond single-consumer-GPU limits where it matters (bigger QLoRA runs in Phase 4, more meaningful-scale RL/PPO/GRPO runs in Phase 2, and paper experiments that need real scale). Keep the from-scratch/single-GPU versions as the fallback and the thing you can explain cold in an interview; use the bigger machines to get results worth putting in a paper or a portfolio README.

---

## Three Goals Running in Parallel

| Goal | What it means |
|------|---------------|
| **Job switch** | Interview-ready depth: transformer internals, open-source tooling, LeetCode Hard, ML system design |
| **Deepen expertise** | Push past what the day job requires: retrieval SOTA (cross/dual-encoders, late-interaction), post-training/RL implemented from scratch, not just used |
| **Research paper** | Submit to KDD (or equivalent), deadline ~February 2027 — likely angle: bridging the Amazon retrieval project with RL/post-training |

A fourth thread runs underneath all of it: becoming a power user of agentic coding tools (Claude Code and similar), starting week 1, applied directly to building every project below.

---

## Three Pillars (interview bar)

| Pillar | What it means |
|--------|---------------|
| **Conceptual depth** | Transformer internals, attention math, scaling laws, alignment, RL (PPO/DPO/GRPO) — implement from scratch and defend every design decision under interview pressure |
| **Open-source tooling** | Port your Bedrock expertise to HuggingFace, LangGraph, PEFT, vLLM, Langfuse — the stack external companies actually use |
| **Hard LeetCode** | Medium fluency + speed early, Hard on Trees/Graphs/DP by the back half — required bar for Google and Meta |

---

## How the Plan Works

Each week runs a **primary** (deeper) and **secondary** (lighter) GenAI track, plus standing tracks that run every week regardless of phase.

| Track | Cadence | Notes |
|-------|---------|-------|
| Primary GenAI | Weekly, heavier | Concept depth first |
| Secondary GenAI | Weekly, lighter | Open-source tooling, retrieval depth, porting from Bedrock |
| **LeetCode** | 5 problems/week through week 18, then timed mocks | Every week, no exceptions |
| **ML System Design** | 1 problem/week starting week 5 | Big tech scale from the start |
| **Agentic Coding** | Ongoing, light | Power-user progression — see [`tracks/agentic-coding.md`](tracks/agentic-coding.md) |
| **Research Paper** | Milestone-based, not weekly-uniform | See [`tracks/research-paper.md`](tracks/research-paper.md) |

**Weekly rhythm:** Fri–Sun are heavy sessions. Spread the week's problems and reading across the days however fits. No day-by-day prescription — track the week.

**To ask "what should I focus on next":** just ask in conversation, or check [`status.md`](status.md) — it's kept current automatically (weekly routine) and manually (when you report progress).

---

## 5 Phases

| Phase | Weeks | Primary | Secondary | Project(s) |
|-------|-------|---------|-----------|------------|
| 1 | 1–6 | Transformer Internals | Retrieval/RAG SOTA (dual-encoder → cross-encoder → hybrid → late-interaction) — **runs in parallel from week 1**, feeds the Amazon retrieval project | nanoGPT + Production RAG system |
| 2 | 7–9 | Post-Training & RL Deep — implement PPO, DPO, GRPO from scratch | Light LoRA/QLoRA toolchain groundwork | P4 begins here (small-scale RL comparison) — also candidate paper substance |
| 3 | 10–12 | Agentic AI (deep, multi-agent + MCP) | — | Multi-agent pipeline (P3) |
| 4 | 13–15 | Fine-Tuning at scale — take Phase 2's winning approach and scale it via QLoRA | Eval + Observability | P4 finishes here (scaled, polished) |
| 5 | 16–19 | Production serving | Interview sprint (mocks, applications) | Deploy everything |

Phase 1 used to be two sequential 4-week phases (transformer, then RAG). They're now parallel from week 1 since the RAG/retrieval depth is immediately useful for the live Amazon project — no reason to wait until week 5 for it. This also means the plan compressed from 20 → 19 weeks even after adding the new RL phase, by consolidating post-training content that used to be scattered across the old Phase 3/4 into one dedicated block.

**P4 is no longer a separate project from the Phase 2 RL work** — it used to be a standalone fine-tuning project bolted onto Phase 4. Now Phase 2 builds it small (PPO/DPO/GRPO from scratch, proving you understand the algorithms) and Phase 4 scales the winning approach up via QLoRA on Amazon compute (proving you can ship it). One continuous project, not two disconnected ones — fewer READMEs to maintain, no learning lost.

---

## The 4 Portfolio Projects

| # | Project | Bedrock/day-job equivalent | Open-source stack |
|---|---------|-------------------|-------------------|
| P1 | nanoGPT from scratch | — | PyTorch |
| P2 | Production RAG System ⭐ | Bedrock Knowledge Bases + Amazon retrieval project | FastAPI · ChromaDB · RAGAS · Langfuse |
| P3 | Multi-Agent Research Pipeline | Strands / AgentCore | LangGraph · Tavily · LangSmith · Anthropic API |
| P4 | RL-Trained + QLoRA Fine-Tuned Model + Benchmark (built Phase 2, scaled Phase 4) | Internal fine-tuning (FLAN-T5/DPO) | HF PEFT/TRL · QLoRA · W&B · Axolotl |

**Polish bar — two tiers, not four projects held to the same standard:** P1 and P2 get the full treatment (README, architecture diagram, demo, write-up) since they're most tied to both the paper and interview-conceptual depth. P3 and P4 need to be functional and clearly documented — a demo GIF or LinkedIn post is a bonus if time allows, not a requirement. This is a deliberate scope reduction to protect the paper and standing tracks from four-way-equal-polish creep.

Phase 5 = deploy + polish P1/P2, tidy up P3/P4. No new project.

---

## Interview Prep (thread throughout — don't save for the end)

### Conceptual — interview-answer depth required
- Derive the attention mechanism from scratch. What are Q, K, V?
- Why does multi-head attention work better than single-head?
- Dual-encoder vs cross-encoder retrieval — architecture, tradeoffs, when to use each as a reranker
- What is late-interaction (ColBERT)? How does it split the difference between dual- and cross-encoders?
- What is RAG and when would you use it vs fine-tuning vs prompting?
- What are LoRA adapters doing mathematically? Why does low-rank decomposition work?
- How does vLLM's PagedAttention improve throughput over naive KV cache allocation?
- What is RLHF? Derive PPO's objective. Why do people prefer DPO over PPO in practice? What does GRPO change?
- How do you evaluate an LLM system in production?
- What are scaling laws and what do they tell us about model training decisions?

### System Design — at Google/Meta/Anthropic scale
- Design a RAG system for a 10M document corpus with sub-200ms p99 latency
- Design a customer support agent with safe escalation to humans
- Design an eval pipeline that catches LLM quality regressions automatically
- How would you reduce LLM API costs by 50% in production?
- Design an LLM serving infrastructure for 100K requests/day with cost optimization
- Design a fine-tuning pipeline for continuous domain adaptation

### Coding — implement from scratch, no frameworks
- Attention mechanism in PyTorch (multi-head, scaled dot-product)
- A cross-encoder scorer and a dual-encoder retriever, and explain the latency/accuracy tradeoff
- Basic RAG pipeline: embed → retrieve → augment → generate
- PPO's clipped objective; DPO's loss; a ReAct agent loop
- Streaming FastAPI endpoint for an LLM

---

## What's Cut

| Topic | Why |
|-------|-----|
| Pretraining from scratch | Hundreds of GPUs. Not a job skill. |
| Kubernetes / MLOps infra | Learn it on the job. |
| Mamba, RWKV, custom architectures | Only if joining a research lab. |
| Multimodal | Additive after you have the core. |
| Diffusion models | Separate track entirely. |

RLHF/PPO implementation was previously cut in favor of "know the theory, DPO wins in practice" — that's reversed now given the RL-depth goal and the paper.

---

## Staying Current (passive, not dedicated study time)

The plan already has enough dedicated resources (Lambert, Raschka, Stanford). The risk isn't missing information, it's missing *time* — so these are meant for dead time (commute, chores), not another study block:

- **[Hugging Face Daily Papers](https://huggingface.co/papers)** — 5-minute skim habit
- **The Batch** (DeepLearning.AI newsletter) — weekly, ~5 min
- **Simon Willison's blog** — practical engineering commentary, already cited for MCP
- **A podcast for commute/gym** (Latent Space, Practical AI) — genuinely free time, not a new obligation

---

## Honest Load Check

Rough weekly hours at this scope: **~15–19 hrs/week** in Phases 1–2, spiking to **~20–26 hrs/week** in weeks 10–16 once paper experiments and the LeetCode Hard ramp overlap. That's heavy on top of a full-time AS3 job — sustained overload for 6-7 weeks straight is a real burnout/abandonment risk, not a hypothetical one.

Two safeguards built into the plan because of this:
1. **`templates/log.md`'s "Time spent" section is a real signal, not decoration.** If logged hours run past ~20/week for 2+ weeks running, that's the trigger to cut scope in the next weekly check-in — not to push through on willpower. See `CLAUDE.md` for how this is wired into the weekly routine.
2. **The paper has an explicit fallback** (see [`tracks/research-paper.md`](tracks/research-paper.md)): if a full draft isn't real by week 16-17, pivot to a workshop submission rather than let the full KDD deadline become a slow-motion miss.

If you notice yourself behind, the honest move is to cut a project's polish bar or the paper's ambition — not to skip LeetCode/system-design (they directly gate interviews) or to just work more hours.

---

## Reference

**GenAI Topics**
- [01 — LLM Foundations](topics/01-llm-foundations.md)
- [02 — Building with LLMs (APIs + RAG + Retrieval SOTA)](topics/02-building-with-llms.md)
- [03 — Agentic AI](topics/03-agentic-ai.md)
- [04 — Fine-Tuning](topics/04-fine-tuning.md)
- [05 — Eval + Production](topics/05-eval-production.md)
- [06 — Post-Training & RL](topics/06-post-training-rl.md)

**Standing Tracks**
- [LeetCode track](tracks/leetcode.md) — pattern progression with Hard ramp
- [ML System Design track](tracks/ml-system-design.md) — weekly problems + design framework
- [Agentic Coding track](tracks/agentic-coding.md) — power-user progression, from week 1
- [Research Paper track](tracks/research-paper.md) — KDD submission, milestone-based

**Progress**
- [status.md](status.md) — current state; kept live, ask "what next?" any time
- [Week-by-week plan](week-by-week.md) — detailed phase breakdown
