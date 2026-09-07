# Week-by-Week Plan

**Context:** You're an AS3 with production LLM experience on Bedrock, currently on a retrieval-systems project. Concepts aren't foreign — you need interview-level depth, the open-source tooling external companies use, RL/post-training at implementation depth, and a KDD-caliber paper by ~February 2027. You have access to larger internal compute for small-scale projects — use it for the fine-tuning and RL phases when single-GPU scale isn't enough.

**Standing tracks every week — non-negotiable:**
- **LeetCode:** see pattern schedule at each phase header — [`tracks/leetcode.md`](tracks/leetcode.md)
- **ML System Design:** 1 problem/week from week 5 — [`tracks/ml-system-design.md`](tracks/ml-system-design.md)
- **Agentic Coding:** ongoing power-user progression, from week 1 — [`tracks/agentic-coding.md`](tracks/agentic-coding.md)
- **Research Paper:** milestone-based, not weekly-uniform — [`tracks/research-paper.md`](tracks/research-paper.md)

---

## Phase 1 — Transformer Internals + Retrieval/RAG SOTA, in parallel (Weeks 1–6)

Go deep on transformer architecture until you can implement and explain every component under pressure. **In true parallel from week 1** (not sequenced after), build retrieval/RAG depth — dual-encoders, cross-encoders, hybrid search, late-interaction — directly useful for your Amazon retrieval project now, not in a month.

**Active projects:** P1 (nanoGPT from scratch — type every line, no copy-paste) + P2 (Production RAG System, built incrementally across all 6 weeks)
**LeetCode:** Arrays & Hashing (weeks 1–2) → Two Pointers + Sliding Window (weeks 3–4) → Stack & Queue (weeks 5-6) — 5 problems/week
**ML System Design:** Not yet — starts week 5
**Agentic Coding:** Wk1–2 daily-driver fundamentals, applied to bootstrapping P1 — see track file
**Research Paper:** Survey phase begins — see track file

---

### Week 1
**Primary — Transformer Architecture:** Watch [Karpathy — Let's Build GPT](https://youtu.be/kCc8FmEb1nY) (2hr). Implement `MultiHeadAttention` and `FeedForward` blocks from scratch. Goal: be able to explain every line you wrote. Start [The Smol Training Playbook](https://huggingface.co/spaces/HuggingFaceTB/smol-training-playbook) (HuggingFace, Aug 2026) as an ongoing companion through Phase 1 — not a week-1 deliverable, just start it. It's the "why" layer behind training decisions (architecture, data, debugging a real 11T-token run) that complements Karpathy's "how."
**Secondary — Retrieval landscape survey:** Skip the HF wrapper-code intro — low-value dedicated study time, pick up `transformers`/`pipeline()` basics just-in-time whenever a task actually needs them. Instead, build a mental map of the retrieval landscape before implementing anything: sparse (BM25) → dense/dual-encoder → cross-encoder/rerankers → late-interaction (ColBERT, multi-vector) → hybrid combinations, plus a look at emerging directions (reasoning-based retrieval, multimodal retrieval, agentic search). Lead with [Benjamin Clavié — P1: I don't use RAG, I just retrieve documents](https://hamel.dev/notes/llm/rag/p1-intro.html) (established approaches first, framed against 2023-era naive RAG) — this is a 7-part series that maps well onto the rest of Phase 1 (see the reading notes in weeks 4-6). The [GenIR survey](https://arxiv.org/abs/2404.14851) is optional, for generative retrieval specifically, if you want that one paradigm in more depth — it's not the right primary landscape resource, it's heavily generative-retrieval-focused rather than a broad survey of established approaches.
**From the P1 slides — flagged for deeper follow-up:** ColBERT/late-interaction (full treatment in week 5, via P4) and multimodal retrieval (CLIP-style dual encoders across text/image — landscape-level only for now; broader multimodal stays out of scope per the plan's cuts unless you want to escalate it).
**Reading:** [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)
**Agentic Coding:** Set up your daily-driver Claude Code workflow (see track file) and use it to scaffold the nanoGPT repo structure.

---

### Week 2
**Primary — Transformer Implementation:** Complete nanoGPT — training loop, cross-entropy loss, sampling with temperature/top-k. Get it training on Shakespeare. Understand why loss goes down.
**Secondary — Dual-encoders in depth:** Now that you have the landscape, implement the first point on it. Embed a small doc set with `sentence-transformers`, store in ChromaDB, run basic retrieval (P2 groundwork). How dual-encoders are trained — contrastive loss, in-batch negatives, hard negative mining. Compare a few off-the-shelf embedding models (E5, BGE, OpenAI/Voyage) — when checking MTEB leaderboard scores, weight out-of-domain/niche-domain subscores over the aggregate average, since that's the better signal of real generalization (see [[evaluating-embedding-models]]). Chunking strategies: fixed-size, sentence-window, semantic.
**Reading:** [Attention Is All You Need](https://arxiv.org/abs/1706.03762) intro + section 3. Cross-reference with your nanoGPT implementation.

---

### Week 3
**Primary — Tokenization + Generation Mechanics:** [Karpathy tokenizer video](https://youtu.be/zduSFxRajkE) (first 45 min). Implement BPE at implementation level. Implement temperature, top-p, top-k sampling yourself.
**Secondary — Cross-encoders:** Architecture — concatenate query+doc, full attention, single relevance score out. **This is literally a transformer encoder classification head** — connect directly to what you built in Primary this week and last. Why cross-encoders are more accurate but too slow for first-stage retrieval; why they're used as rerankers instead (monoT5, Cohere Rerank, BGE-reranker). Add a reranking stage to your P2 pipeline.
**Reading:** [HuggingFace NLP Course Ch 5–6](https://huggingface.co/learn/nlp-course/chapter5/1) — datasets and tokenization internals

---

### Week 4
**Primary — Alignment: RLHF, DPO, Scaling Laws (conceptual primer):** Watch [Nathan Lambert — RLHF series](https://www.youtube.com/@natolambert) ("Understanding RLHF," "DPO explained"). Read [InstructGPT](https://arxiv.org/abs/2203.02155) sections 1–3 and [Chinchilla](https://arxiv.org/abs/2203.15556) abstract + conclusion. This is the conceptual layer — Phase 2 goes to implementation depth on this.
**Secondary — Hybrid search + reranking pipeline:** Add BM25 (keyword) + vector (semantic) hybrid search to P2. Wire the cross-encoder reranker from week 3 into the full pipeline. Understand *why* hybrid beats either alone.
**Reading:** [DPO paper](https://arxiv.org/abs/2305.18290) — you've worked with it in production; now understand the derivation; [Clavié — P5: RAG with Multiple Representations](https://hamel.dev/notes/llm/rag/p5_map.html) — directly on-topic for this week's hybrid pipeline
**Agentic Coding:** Move to subagent/multi-agent workflows (see track file) — apply to building out P2's pipeline stages in parallel.

---

### Week 5
**Primary — nanoGPT polish:** Clean training run, push to GitHub with README. Can implement and explain every component cold. **End of primary arc for Phase 1.**
**Secondary — SOTA / multi-vector + late-interaction retrieval (the topic you flagged from P1 — full treatment here):** Start with [Clavié — P4: Late Interaction Models For RAG](https://hamel.dev/notes/llm/rag/p4_late_interaction.html) as the accessible entry point, then go deeper with the ColBERT paper. Multi-vector retrieval as the general idea (multiple vectors per doc/query instead of one) — ColBERT's late-interaction/max-sim scoring is the prominent instance; where it sits between dual- and cross-encoders on the accuracy/speed curve, and at what storage cost. **Hands-on: use `pylate` (not a from-scratch reimplementation) to index P2's docs with a real late-interaction model (e.g. GTE-ModernColBERT) and compare against your week 1-2 dual-encoder baseline** — see [[modern-late-interaction-models]] in `concepts/`. SPLADE — learned sparse retrieval. Read enough to compare tradeoffs across bi-encoder / multi-vector-late-interaction / cross-encoder / hybrid for a given latency budget — this is an interview favorite and directly relevant to your Amazon project. **Multimodal retrieval (landscape-level, the other topic you flagged):** CLIP-style dual encoders across text/image — same dual-encoder contrastive-training idea from week 2, just cross-modal. This stays conceptual-only; hands-on multimodal implementation is still out of scope per the plan's cuts.
**Reading:** [ColBERT paper](https://arxiv.org/abs/2004.12832) intro + architecture; [ModernBERT](https://arxiv.org/abs/2412.13663) (the backbone ModernColBERT builds on — skim, don't need full depth); [SPLADE paper](https://arxiv.org/abs/2107.05720) abstract + section 2; [CLIP paper](https://arxiv.org/abs/2103.00020) abstract + architecture (for multimodal retrieval — skim, not implement)
**ML System Design starts:** Design a conversational chatbot API — see track file.

---

### Week 6
**Primary — buffer / Phase 2 prep:** Re-read [RLHF/DPO papers] you covered in week 4 now that nanoGPT is done — you have a working transformer to reason about concretely. Skim [PPO paper](https://arxiv.org/abs/1707.06347) intro, no implementation yet (that's Phase 2).
**Secondary — RAGAS Evaluation + wrap-up:** Add evaluation harness to P2: 30 Q&A pairs, RAGAS faithfulness + answer relevancy + context recall automated. Add Langfuse tracing. Consider building your 30 Q&A pairs FreshStack-style (see [[freshstack-benchmark-creation]]) — mine real questions relevant to your domain, extract the atomic facts an answer needs, check whether retrieval covers all of them — a domain-specific eval set like this is more convincing than generic pairs, both in the README and later in the paper. Write P2's GitHub README with an explicit comparison table (dual-encoder vs cross-encoder vs hybrid vs late-interaction) tying back to your Amazon retrieval work. **P2 done.**
**Reading:** [RAGAS paper](https://arxiv.org/abs/2309.15217) sections 1–3; [Clavié — P2: Modern IR Evals For RAG](https://hamel.dev/notes/llm/rag/p2-evals.html) — its point on evaluating coverage/diversity rather than just RAGAS-style single-answer metrics is directly relevant to this week's eval harness (see [[traditional-vs-rag-era-retrieval-eval]] in `concepts/` for the synthesized comparison). If you want the bridge into Phase 2's RL work and the paper's likely angle, read [Clavié — P3: Optimizing Retrieval with Reasoning Models](https://hamel.dev/notes/llm/rag/p3_reasoning.html) too — covers Promptriever and Rank1 (see [[instruction-based-retrievers]] in `concepts/`), a dual-encoder/cross-encoder pair for instruction-following retrieval that's close, concrete prior art for whatever the paper's angle ends up being.
**Research Paper:** Target topic lock by end of this week or next — see track file. Retrieval SOTA work this phase should directly inform the decision.
**End of phase:** nanoGPT on GitHub. P2 (Production RAG System) live with RAGAS scores and a retrieval-architecture comparison. Both explainable cold in an interview.

---

## Phase 2 — Post-Training & RL Deep (Weeks 7–9)

Implement PPO, DPO, and GRPO from scratch — not just read the papers or call a trainer. You know DPO conceptually from production (Amazon) and from Phase 1's primer; now build the full post-training pipeline (SFT → reward model → RL) at implementation depth. This phase likely produces the technical core of the paper if the RL angle wins out.

**Active project:** P4 begins here — RL implementations (PPO / DPO / GRPO on a small model) — candidate paper substance. Phase 4 scales the winning approach up; this isn't a separate project from that.

**Pick the comparison task now, in week 7, not later:** GRPO specifically needs a *verifiable-reward* task (its whole premise), so use one for all three algorithms to keep the comparison apples-to-apples — grade-school math (GSM8K-style, correctness is checkable) or a simple code-correctness task (does it pass the test) both work well and are cheap to score. Train the week 7 reward model against this same task.
**LeetCode:** Binary Search (weeks 7–8) → Linked Lists starts (week 9) — 5 problems/week
**ML System Design:** semantic document search (wk6 catch-up if needed) → RAG at 10M-doc scale (wk7) → RAG eval pipeline (wk8) → customer support agent (wk9)
**Agentic Coding:** Wk5–8 window — build a personal MCP server (see track file), running in parallel with this phase

---

### Week 7
**Primary — Reward Modeling + PPO:** Read [InstructGPT](https://arxiv.org/abs/2203.02155) full + [PPO paper](https://arxiv.org/abs/1707.06347) sections 1–3. Implement a reward model (small classifier head on a small LM) — for the math/code task chosen above, this can just be the programmatic checker (correct/incorrect), you don't need a learned reward model unless you want to compare that too. Implement PPO's clipped surrogate objective from scratch — even a toy RL environment first (CartPole-style) to get the mechanics right before applying to text generation.
**Secondary — LoRA/QLoRA toolchain groundwork:** [PEFT docs — LoRA quickstart](https://huggingface.co/docs/peft/quicktour). Run the LoRA example on a small model. This groundwork feeds Phase 4's full fine-tune.
**Reading:** [rlhfbook.com](https://rlhfbook.com/) chapters on reward modeling + PPO; [PPO paper](https://arxiv.org/abs/1707.06347) — the clipping mechanism in detail
**Optional backfill:** if the policy-gradient math feels shaky, watch [Stanford CS234](https://www.youtube.com/playlist?list=PLoROMvodv4rN4wG6Nk6sNpTEbuOSosZdX) lectures 1–6 (classical RL foundations — MDPs, value functions, policy gradient theorem) before continuing. Not required if PPO's mechanics already make sense.

---

### Week 8
**Primary — PPO on a Small LM + DPO derivation:** Apply your PPO implementation to a small LM with your week 7 reward model — full RLHF loop end to end, even if the model is tiny. Then derive DPO from the RLHF objective (the closed-form solution that skips the reward model). Implement DPO from scratch (loss function, not just `TRL`'s trainer) and compare against your PPO run on the same preference data.
**Secondary — QLoRA environment:** Set up QLoRA (use Amazon compute here if the local GPU is limiting). Load a 7B+ model in 4-bit, verify it trains.
**Reading:** [DPO paper](https://arxiv.org/abs/2305.18290) sections 3–4 — the full derivation

---

### Week 9
**Primary — GRPO + Reasoning RL:** Read the [DeepSeek-R1 paper](https://arxiv.org/abs/2501.12948) (or successor) for GRPO — how it drops the value network PPO needs, why that matters for reasoning tasks. Implement GRPO from scratch on your small-LM setup from week 8; compare PPO vs DPO vs GRPO on the same task — this comparison is a strong paper figure if the RL angle is chosen. Sebastian Raschka's [Build a Reasoning Model From Scratch](https://sebastianraschka.com/blog/) is a strong hands-on companion for this week specifically.
**Secondary — Fine-tuning prep:** Format a domain dataset (Alpaca-style) for Phase 4. Ideally something adjacent to the retrieval project or the RL comparison above.
**Reading:** [GRPO / DeepSeek-Math paper](https://arxiv.org/abs/2402.03300) — the GRPO objective section; skim [rlhfbook.com](https://rlhfbook.com/)'s RLVR/reasoning chapter and note that DAPO/GSPO/GFPO/CISPO exist as GRPO successors (awareness level — see [Topic 6](topics/06-post-training-rl.md))
**End of phase:** PPO, DPO, and GRPO all implemented from scratch and benchmarked against each other on the same task. This is the phase most likely to feed the paper directly.

---

## Phase 3 — Agentic AI Deep (Weeks 10–12)

Build multi-agent architecture using open-source tools — the open-source equivalent of your Strands/AgentCore experience.

**Active project:** P3 (Multi-Agent Research Pipeline)
**LeetCode:** Linked Lists (week 10) → Trees BFS+DFS (weeks 11–12) — **Hard ramp begins: 3 Medium + 2 Hard/week**
**ML System Design:** multi-agent research assistant (wk10) → content moderation pipeline (wk11) → code review assistant (wk12)
**Agentic Coding:** Ongoing — default to agentic workflows for building P3 itself; this is the most natural project to dogfood multi-agent orchestration on

---

### Week 10
**Multi-Agent Architecture:** Build P3 — Supervisor → Planner → Researcher (Tavily) → Writer pipeline in LangGraph. Pass state through the graph, handle handoffs. Work through [DeepLearning.AI: AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/) lessons 1–3 in parallel if the framework is unfamiliar.
**Reading:** [Anthropic — Building Effective Agents](https://www.anthropic.com/research/building-effective-agents)

---

### Week 11
**Agent Reliability:** Add failure handling — max retries, bad tool output recovery, fallback paths, human-in-the-loop approval. Add LangSmith traces with per-agent-step spans.
**Reading:** [AutoGen paper](https://arxiv.org/abs/2308.08155) architecture section — compare to your AgentCore experience.

---

### Week 12
**MCP + Wrap-up:** Build an MCP server wrapping a real API (if you didn't already via the Agentic Coding track). Write a clear P3 README with what it does and LangSmith trace screenshots — P3 is a "functional + documented" project (see the polish-bar note in README.md), so a full demo recording/architecture diagram is a bonus if time allows, not required.
**Reading:** [MCP specification](https://modelcontextprotocol.io/introduction)
**End of phase:** P3 live on GitHub, documented well enough that you can walk through it in an interview.

---

## Phase 4 — Fine-Tuning at Scale (P4 finishes) + Eval/Observability (Weeks 13–15)

**This is P4's second half, not a new project.** Phase 2 proved you understand PPO/DPO/GRPO from scratch on a small model. Now take whichever approach won that comparison and scale it up via full QLoRA on a bigger base model, using Amazon compute where a single consumer GPU wouldn't cut it. Eval/observability run in parallel because you need them to measure whether it actually worked.

**Active project:** P4 scale-up (from Phase 2) + eval harness on P2
**LeetCode:** Graphs (weeks 13–14) → DP 1D+2D starts (week 15) — continue Hard: 3 Medium + 2 Hard/week
**ML System Design:** fine-tuning pipeline (wk13) → recommendation system with LLMs (wk14) → LLM serving infra (wk15)

---

### Week 13
**QLoRA Fine-Tune Run:** Full training run with Axolotl, using Phase 2's winning approach (DPO or GRPO, whichever benchmarked better) — iterate on dataset quality, LR, rank. Log with W&B. Run at least 2 configurations, including at least one at a scale your local GPU couldn't handle (Amazon compute).
**Reading:** [Axolotl config docs](https://github.com/axolotl-ai-cloud/axolotl)

---

### Week 14
**Before/After Benchmark:** 20 test prompts, base vs fine-tuned, scored with LLM-as-judge (or the programmatic checker from Phase 2, if you kept the same verifiable-reward task at scale — even better, since it's not just vibes-based judging). HF model card, push adapter to HF Hub. **P4 done** — small-scale algorithm comparison (Phase 2) + scaled production-quality result (here), one continuous project.
**Reading:** [LIMA paper](https://arxiv.org/abs/2305.11206) — data quality > quantity

---

### Week 15
**Observability + Eval Harness:** Add Langfuse tracing to P3, prompt versioning. Build eval harness for P2 — 50 Q&A pairs, RAGAS automated, `promptfoo` regression detection.
**Reading:** [Judging LLM-as-a-Judge](https://arxiv.org/abs/2306.05685)
**End of phase:** P4 on HF Hub, documented (results table, model card). Full eval harness on P2. P3 and P4 are both "functional + documented" tier — P4 likely ends up more thoroughly written up anyway since the paper draws on the same results, but that's a byproduct of the paper work, not an extra polish pass to schedule separately.

---

## Phase 5 — Production Serving + Interview Sprint (Weeks 16–19)

No new projects. Deploy what exists. From week 18 the primary focus shifts to interview prep.

**LeetCode:** Heap + Priority Queue (weeks 17–18) → timed mock session (week 19)
**ML System Design:** prompt management + A/B testing (wk16) → real-time writing assistant (wk17) → multimodal document Q&A (wk18) → mock interview ×2 (wk19)

---

### Week 16
**Primary — vLLM + Inference Optimization:** Serve your P4 model with vLLM. Benchmark throughput vs naive HF inference. Understand PagedAttention and continuous batching by watching GPU utilization, not just conceptually.
**Secondary — Interview Prep begins:** Start the conceptual Q&A list in the README. One topic per session — explain out loud, record yourself, watch it back.
**Reading:** [PagedAttention paper](https://arxiv.org/abs/2309.06180) abstract + section 2

---

### Week 17
**Primary — Production Deployment:** Dockerize P2 (FastAPI + ChromaDB + Langfuse), add LiteLLM proxy, deploy to Modal or HF Spaces. Demo GIFs for P1 and P2's READMEs (the full-polish tier); P3/P4 just need their existing documentation to be current.
**Secondary — Interview Prep:** System design questions, written up as documents in `log/`.
**Reading:** [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)

---

### Week 18
**Interview Prep — System Design:** Timed mock sessions — RAG at scale, agent with HITL, eval pipeline design, LLM serving infra, RL/post-training pipeline design (new, given Phase 2).
**GitHub polish:** P1/P2 clean with architecture diagrams and live demo links; P3/P4 just need current, accurate READMEs. LinkedIn updated (P1/P2, and the paper if it's far enough along to mention).
**Reading:** Review all 6 topic files, fill any conceptual gaps.

---

### Week 19
**Interview Prep — Coding under time pressure:** Implement attention from scratch, a cross-encoder + dual-encoder scorer, PPO's clipped objective, ReAct loop, streaming FastAPI endpoint.
**Applications:** Send applications, tailored per company (Google: scale + research; Meta: systems + experimentation; Anthropic: alignment + model internals; Apple: privacy + on-device; Netflix: personalization + A/B).
**Paper:** Should be in the writing/polish window by now — see track file for the parallel timeline.
**Deliverable:** Interview-ready. All 4 projects live. Applications sent. Paper in final polish ahead of the ~February KDD deadline.
