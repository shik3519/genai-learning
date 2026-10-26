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
Week 1 (carried forward — 8th calendar week running) — Phase 1 (Transformer Internals + Retrieval/RAG SOTA, in parallel). Week of Oct 26–Nov 1. Not advancing to Week 2: there is still no log entry for any week since Sept 13 — the most recent log remains `log/2026-09-13.md` (days 1-6 of week 1). With no entry to show otherwise, none of Week 1's deliverables can be assumed to have moved: nanoGPT `MultiHeadAttention`/`FeedForward` still not started, LeetCode Arrays & Hashing still not started, the Stage 1 retrieval experiment (BM25 + dual-encoder on SciFact) still not started, agentic-coding daily-driver setup still not done. **This is the seventh consecutive weekly check-in (Sept 14, 21, 28, Oct 5, Oct 12, Oct 19, Oct 26) carrying Week 1 forward with nothing new to show — seven weeks of calendar time against one plan-week of logged progress.** The Oct 19 check-in explicitly named a seventh carry-forward without a real conversation or a logged session as the point where the mechanical carry-forward itself becomes the problem rather than the right move — that point has now arrived. This check-in still carries Week 1 forward once more, because the routine has no evidence of movement to advance on and leaving status.md stale would be worse than an honest repeat — but it is doing so under explicit protest, not as business-as-usual, and this is flagged for a direct check-in with Shikhar rather than deferred to an eighth pass.

## What I've completed
- Secondary (reading): all of Clavié's "Stop Saying RAG Is Dead" series, P1 through P5 — full retrieval landscape, evals, reasoning-based retrieval, late-interaction, multi-representation
- Ahead of schedule: Sebastian Raschka's *Build a Reasoning Model From Scratch*, first 2 videos (this is Phase 2 content, weeks 7-9)
- YC Paper Club's "Why The Harness Matters More Than The Model" — filed as [[agent-harnesses]]
- Nothing built/coded yet on any track (see the pattern note below)

## What I'm actively working on
- **Fourth flag in a row, and the one the Oct 19 check-in said would be the last mechanical repeat:** seven weekly check-ins running (Sept 14, 21, 28, Oct 5, Oct 12, Oct 19, now Oct 26) have found zero new logged progress since `log/2026-09-13.md`. Oct 5, Oct 12, and Oct 19 all named this as needing a direct scope/re-planning conversation rather than another carry-forward — that still hasn't visibly happened. The plan's Week 1 deliverables (nanoGPT attention/FFN, Arrays & Hashing, Stage 1 retrieval experiment, agentic-coding setup) are unchanged from six weeks ago. The question is no longer "what to study next" — it's whether the 19-week calendar-mapped plan still fits actual available time, and if not, whether/how to compress, replan, or reset the start date. This is the point this routine was told to surface explicitly rather than quietly repeat again.
- Priority if picking back up: Karpathy "Let's Build GPT" + implementing `MultiHeadAttention`/`FeedForward` from scratch (nanoGPT, P1) — still the single most-stalled, most-blocking item (everything else in Phase 1 assumes it). Hold off on any further new resources (including Raschka's book, Phase 2 material) until this lands.
- Secondary: retrieval landscape reading is done (P1-P5) — next concrete step is Stage 1 of the comparison experiment (BM25 + dual-encoder on SciFact, see `projects/mini-rag-bot/notes.md`), not more reading.
- Standing: LeetCode — Arrays & Hashing (5 problems), still not started.
- Agentic Coding: daily-driver Claude Code workflow setup, still not started — meant to scaffold P1, not follow it, so pair it with the nanoGPT push rather than sequencing after.
- ML System Design: not yet — starts week 5, no action needed.
- **Research paper — drift is now significant, not just worth naming:** still nominally inside its week 1-6 survey/lit-review milestone, but with six calendar weeks of zero logged plan-progress overall, the week 6-7 topic-lock milestone is now well past its original target with nothing locked. Not yet at the week 16-17 workshop-fallback decision point, but the gap between the nominal milestone and actual progress keeps widening — this belongs in the same scope conversation flagged above, not as a separate concern.
- **Logging gap, now spanning six full weeks:** no log entry exists for any week from Sept 14–20 through Oct 12–18 — the "logging progress" workflow hasn't been followed since Sept 13. Worth logging even a "did nothing this week" entry going forward, since the load check and this weekly recommendation both depend on that data existing.

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
Still no new log entry since `log/2026-09-13.md` (days 1-6 of week 1, ~4 hrs total, all reading/watching) — same single real data point as the last six check-ins (`log/2026-05-07.md` remains an empty unused template, not a data point). Hours are not the concern here; if anything it's the opposite of overload — the risk is near-zero engagement, not too much. This has now persisted for seven consecutive weekly check-ins (six full unlogged calendar weeks against one plan-week of logged progress), well past the point where it's a signal in its own right rather than something to just re-check again next week — see the flag under "What I'm actively working on" above. Re-check once an entry covering the Sept 14–Oct 25 window lands, but the absence of data is no longer a reason to defer the scope/re-planning conversation — it's the reason to have it.

## Recent logs
- [2026-09-13](../log/2026-09-13.md)

## What I want to focus on next (optional)
<!-- Leave blank for a cold recommendation based on the above -->
