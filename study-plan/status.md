# Current Status

> Update this file as you go. Share it when asking "what should I focus on next?" — this is the context needed for a sharp recommendation.

---

## Starting baseline (August 2026)

**Production experience (Bedrock ecosystem):**
- Large-scale LLM systems: ad copy generation, multi-agent chatbot (Strands/AgentCore)
- Prompt engineering, LLM-as-judge, prompt caching: production experience
- RAG (Bedrock Knowledge Bases): production experience
- Fine-tuning FLAN-T5, DPO (mentorship): some hands-on
- Agents (Strands/AgentCore): production experience
- 7 published papers (workshops + ECNLP@KDD oral, NeurIPS workshop)

**Gaps going in:**
- Transformer internals: conceptually weak, needs interview-depth treatment
- Open-source stack: HuggingFace, LangGraph, PEFT, vLLM, Langfuse — largely new
- LeetCode: can solve Medium slowly, needs speed + Hard fluency
- Production serving: vLLM, Docker deployment — new territory
- Post-training/RL at implementation depth: know DPO conceptually from production, but PPO/GRPO from scratch is new
- Retrieval SOTA: production RAG experience (Bedrock KBs), but cross-encoder/late-interaction/SPLADE depth is new

**Current context (September 2026):**
- Working a retrieval-systems project at Amazon — Phase 1's retrieval/RAG SOTA track is deliberately front-loaded to feed this
- Have access to larger internal Amazon compute for small-scale projects — use for Phase 2 (RL) and Phase 4 (fine-tuning) when local GPU is limiting
- Targeting a KDD (or equivalent) paper submission, ~February 2027 — see [`tracks/research-paper.md`](tracks/research-paper.md)

---

## Current week
Week 1 — Phase 1 (Transformer Internals + Retrieval/RAG SOTA, in parallel), starting week of 2026-09-07.

## What I've completed
Nothing yet — tracking restarts here as of 2026-09-05.

## What I'm actively working on
- Primary: Karpathy "Let's Build GPT" + implementing `MultiHeadAttention`/`FeedForward` from scratch (nanoGPT, P1)
- Secondary: HuggingFace intro + dual-encoder fundamentals — load GPT-2, tokenize, run inference; embed a small doc set and run basic retrieval on ChromaDB (P2 groundwork)
- Standing: LeetCode — Arrays & Hashing (5 problems this week)
- Agentic Coding: set up daily-driver Claude Code workflow, use it to scaffold P1

## Where I'm stuck or fuzzy
<!-- Be specific — "I understand attention conceptually but can't implement scaled dot-product from scratch" is more useful than "attention" -->

## Confidence levels (1–5)
| Topic | Confidence | Notes |
|-------|------------|-------|
| Transformer internals (implement from scratch) | | |
| Tokenization (BPE, implement level) | | |
| Retrieval architectures (dual-encoder, cross-encoder, ColBERT, SPLADE) | | |
| Alignment: RLHF, DPO, scaling laws (conceptual) | | |
| Post-training/RL implemented from scratch (PPO, DPO, GRPO) | | |
| RAG (open-source stack: ChromaDB, RAGAS, Langfuse) | | |
| Agentic AI (LangGraph, multi-agent) | | |
| Fine-Tuning (LoRA/QLoRA, PEFT, Axolotl) | | |
| Eval + Observability (Langfuse, LLM-as-judge depth) | | |
| Production serving (vLLM, Docker) | | |
| Agentic coding power-user (Claude Code workflows) | | |
| LeetCode — Medium speed | | |
| LeetCode — Hard (Trees, Graphs, DP) | | |
| ML System Design | | |

## Projects status
| Project | Status | GitHub |
|---------|--------|--------|
| P1 — nanoGPT | Not started | |
| P2 — RAG System | Not started | |
| P3 — Multi-Agent Pipeline | Not started | |
| P4 — Fine-Tuned Model | Not started | |
| RL implementations (PPO/DPO/GRPO) | Not started | |
| Research paper (KDD, ~Feb 2027) | Topic not yet locked | |

## Recent logs
<!-- Link your last 2-3 weekly logs here -->

## What I want to focus on next (optional)
<!-- Leave blank for a cold recommendation based on the above -->
