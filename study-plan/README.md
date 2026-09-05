# GenAI Study Plan — Interview Ready by End of 2026

**Target:** Applied Scientist at Apple, Netflix, Google, Meta, Anthropic  
**Timeline:** 20 weeks (August → December 2026), flex to Q1 2027  
**Starting point:** AS3 with production LLM experience on Bedrock. Concepts familiar but not interview-deep. Open-source stack (HuggingFace, LangGraph, vLLM, PEFT) is largely new.

---

## Three Pillars

| Pillar | What it means |
|--------|---------------|
| **Conceptual depth** | Transformer internals, attention math, scaling laws, alignment — not "I know how RAG works" but able to implement from scratch and defend every design decision under interview pressure |
| **Open-source tooling** | Port your Bedrock expertise to HuggingFace, LangGraph, PEFT, vLLM, Langfuse — the stack external companies actually use |
| **Hard LeetCode** | Medium fluency + speed by week 8, Hard on Trees/Graphs/DP by week 16 — required bar for Google and Meta |

---

## How the Plan Works

Each week runs **2 parallel GenAI tracks** (primary = deeper, secondary = lighter) plus two standing tracks every week.

| Track | Cadence | Notes |
|-------|---------|-------|
| Primary GenAI | Weekly, heavier | Concept depth first |
| Secondary GenAI | Weekly, lighter | Open-source tooling, porting from Bedrock |
| **LeetCode** | 5 problems/week (weeks 1–8), Hard ramp (weeks 9–16), mocks (weeks 17–20) | Every week, no exceptions |
| **ML System Design** | 1 problem/week starting week 5 | Big tech scale from the start |

**Weekly rhythm:** Fri–Sun are your heavy sessions. Spread the week's problems and reading across the days however fits. No day-by-day prescription — track the week.

**To ask "what should I focus on next":** update [`status.md`](status.md) and share it.

---

## 5 Phases

| Phase | Weeks | Primary | Secondary | Project(s) |
|-------|-------|---------|-----------|------------|
| 1 | 1–4 | Transformer Internals | HuggingFace Ecosystem | nanoGPT |
| 2 | 5–8 | RAG (production depth) | LangGraph single agent | Production RAG system |
| 3 | 9–12 | Agentic AI (deep) | Fine-Tuning intro (LoRA/QLoRA toolchain) | Multi-agent pipeline + first fine-tune |
| 4 | 13–16 | Fine-Tuning (QLoRA end-to-end) | Eval + Observability | Fine-tuned model + eval harness |
| 5 | 17–20 | Production serving | Interview sprint | Deploy everything |

---

## The 4 Portfolio Projects

These are the open-source equivalents of what you've already built on Bedrock.

| # | Project | Bedrock equivalent | Open-source stack |
|---|---------|-------------------|-------------------|
| P1 | nanoGPT from scratch | — | PyTorch |
| P2 | Production RAG System ⭐ | Bedrock Knowledge Bases | FastAPI · ChromaDB · RAGAS · Langfuse |
| P3 | Multi-Agent Research Pipeline | Strands / AgentCore | LangGraph · Tavily · LangSmith · Anthropic API |
| P4 | LoRA Fine-Tuned Model + Benchmark | Internal fine-tuning (FLAN-T5/DPO) | HF PEFT · QLoRA · W&B · Axolotl |

Phase 5 = deploy + polish all four. No new project.

---

## Interview Prep (thread throughout — don't save for month 5)

### Conceptual — interview-answer depth required
- Derive the attention mechanism from scratch. What are Q, K, V?
- Why does multi-head attention work better than single-head?
- What is RAG and when would you use it vs fine-tuning vs prompting?
- What are LoRA adapters doing mathematically? Why does low-rank decomposition work?
- How does vLLM's PagedAttention improve throughput over naive KV cache allocation?
- What is RLHF? What is DPO and why do people prefer it over PPO?
- How do you evaluate an LLM system in production?
- What are scaling laws and what do they tell us about model training decisions?
- What is the KV cache and when does it become a bottleneck?
- What is constitutional AI? How does it differ from RLHF?

### System Design — at Google/Meta/Anthropic scale
- Design a RAG system for a 10M document corpus with sub-200ms p99 latency
- Design a customer support agent with safe escalation to humans
- Design an eval pipeline that catches LLM quality regressions automatically
- How would you reduce LLM API costs by 50% in production?
- Design an LLM serving infrastructure for 100K requests/day with cost optimization
- Design a fine-tuning pipeline for continuous domain adaptation

### Coding — implement from scratch, no frameworks
- Attention mechanism in PyTorch (multi-head, scaled dot-product)
- Basic RAG pipeline: embed → retrieve → augment → generate
- ReAct agent loop from scratch
- Streaming FastAPI endpoint for an LLM
- RAGAS faithfulness metric from scratch

---

## What's Cut

| Topic | Why |
|-------|-----|
| Pretraining from scratch | Hundreds of GPUs. Not a job skill. |
| RLHF/PPO implementation | Know the theory deeply. DPO is simpler and wins in practice. |
| Kubernetes / MLOps infra | Learn it on the job. |
| Mamba, RWKV, custom architectures | Only if joining a research lab. |
| Multimodal | Additive after you have the core. |
| Diffusion models | Separate track entirely. |

---

## Reference

**GenAI Topics**
- [01 — LLM Foundations](topics/01-llm-foundations.md)
- [02 — Building with LLMs (APIs + RAG)](topics/02-building-with-llms.md)
- [03 — Agentic AI](topics/03-agentic-ai.md)
- [04 — Fine-Tuning](topics/04-fine-tuning.md)
- [05 — Eval + Production](topics/05-eval-production.md)

**Standing Tracks**
- [LeetCode track](tracks/leetcode.md) — pattern progression with Hard ramp
- [ML System Design track](tracks/ml-system-design.md) — weekly problems + design framework

**Progress**
- [status.md](status.md) — current state; update and share when asking "what next?"
- [Week-by-week plan](week-by-week.md) — detailed phase breakdown
