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
Week 1 (carried forward — 4th calendar week running) — Phase 1 (Transformer Internals + Retrieval/RAG SOTA, in parallel). Week of Sept 28–Oct 4. Not advancing to Week 2: there is still no log entry for the week of Sept 14–20 or Sept 21–27 — the most recent log remains `log/2026-09-13.md` (days 1-6 of week 1). With no entry to show otherwise, none of Week 1's deliverables can be assumed to have moved: nanoGPT `MultiHeadAttention`/`FeedForward` still not started, LeetCode Arrays & Hashing still not started, the Stage 1 retrieval experiment (BM25 + dual-encoder on SciFact) still not started, agentic-coding daily-driver setup still not done. Same Week 1 deliverables carry forward again — this is now the third consecutive weekly check-in with nothing new to show.

## What I've completed
- Secondary (reading): all of Clavié's "Stop Saying RAG Is Dead" series, P1 through P5 — full retrieval landscape, evals, reasoning-based retrieval, late-interaction, multi-representation
- Ahead of schedule: Sebastian Raschka's *Build a Reasoning Model From Scratch*, first 2 videos (this is Phase 2 content, weeks 7-9)
- YC Paper Club's "Why The Harness Matters More Than The Model" — filed as [[agent-harnesses]]
- Nothing built/coded yet on any track (see the pattern note below)

## What I'm actively working on
- **Priority — carried over a third time, now the most urgent item by far:** Karpathy "Let's Build GPT" + implementing `MultiHeadAttention`/`FeedForward` from scratch (nanoGPT, P1). Four calendar weeks in with no code written yet — hold off on any further new resources (including Raschka's book, which is Phase 2 material anyway) until this actually lands. If this doesn't move by the next check-in, worth naming explicitly as a scope/re-planning conversation rather than carrying it forward a fourth time.
- Secondary: retrieval landscape reading is done (P1-P5) — next concrete step is Stage 1 of the comparison experiment (BM25 + dual-encoder on SciFact, see `projects/mini-rag-bot/notes.md`), not more reading.
- Standing: LeetCode — Arrays & Hashing (5 problems), still not started.
- Agentic Coding: daily-driver Claude Code workflow setup, still not started — meant to scaffold P1, not follow it, so pair it with the nanoGPT push rather than sequencing after.
- ML System Design: not yet — starts week 5, no action needed.
- Research paper: not flagged as stale on content yet — still inside its week 1-6 survey/lit-review milestone, and the Clavié P1-P5 reading already logged doubles as groundwork for the week 6-7 topic-lock decision. But it's riding on the same general inactivity as everything else below, and the week 6-7 topic-lock milestone is getting closer in calendar time than the stalled Week 1 progress suggests — worth a straight look at whether ~week 6-7 (in plan-weeks) is still realistic given four calendar weeks have produced one week of plan progress.
- **Logging gap, now spanning two full weeks:** no log entry exists for either the week of Sept 14–20 or Sept 21–27 — the "logging progress" workflow hasn't been followed since Sept 13. There's no record of what happened (if anything) in either week. Worth logging even a "did nothing this week" entry going forward, since the load check and this weekly recommendation both depend on that data existing.

## Where I'm stuck or fuzzy
Nothing identified yet — haven't gotten deep enough into implementation on any track to know where the real sticking points are. That's exactly why the primary/hands-on work needs to happen next, not more reading.

## Confidence levels (1–5)
| Topic | Confidence | Notes |
|-------|------------|-------|
| Transformer internals (implement from scratch) | | |
| Tokenization (BPE, implement level) | | |
| Retrieval architectures (dual-encoder, cross-encoder, multi-vector/ColBERT, SPLADE, generative retrieval) | | |
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
| Project | Status | Polish tier | GitHub |
|---------|--------|--------|--------|
| P1 — nanoGPT | Not started | Full | |
| P2 — RAG System | Not started | Full | |
| P3 — Multi-Agent Pipeline | Not started | Functional + documented | |
| P4 — RL-trained + QLoRA model (starts Phase 2, scales Phase 4 — one project, not two) | Not started | Functional + documented (naturally thorough via the paper) | |
| Research paper (KDD, ~Feb 2027) | Topic not yet locked | — | |

## Load check
Still no new log entry since `log/2026-09-13.md` (days 1-6 of week 1, ~4 hrs total, all reading/watching) — same single real data point as the last two check-ins (`log/2026-05-07.md` remains an empty unused template, not a data point). Hours are not the concern here; if anything it's the opposite of overload — the risk is near-zero engagement, not too much, and it's now persisted long enough (two full unlogged weeks, ~4 calendar weeks against 1 plan-week of progress) that it's worth treating as a signal in its own right rather than just re-checking again next week. Re-check once an entry covering the Sept 14–Oct 4 window lands.

## Recent logs
- [2026-09-13](../log/2026-09-13.md)

## What I want to focus on next (optional)
<!-- Leave blank for a cold recommendation based on the above -->
