# Week-by-Week Plan

**Context:** You're an AS3 with production LLM experience on Bedrock. Concepts aren't foreign — you need interview-level depth and the open-source tooling that external companies use. Every week: primary (deeper conceptual work) + secondary (open-source tooling, porting from Bedrock).

**Standing tracks every week — non-negotiable:**
- **LeetCode:** see pattern and Hard ramp schedule at each phase header
- **ML System Design:** 1 problem/week from week 5. Framework + problems in [`tracks/ml-system-design.md`](tracks/ml-system-design.md)

---

## Phase 1 — Transformer Internals + HuggingFace Ecosystem (Weeks 1–4)

Go deep on transformer architecture until you can implement and explain every component under pressure. In parallel, get hands-on with the HuggingFace ecosystem — the tooling layer that sits on top of everything external companies build.

**Active project:** P1 (nanoGPT from scratch — type every line, no copy-paste)  
**LeetCode:** Arrays & Hashing (weeks 1–2) → Two Pointers + Sliding Window (weeks 3–4) — 5 problems/week, goal is speed not just correctness  
**ML System Design:** Not yet — starts week 5

---

### Week 1
**Primary — Transformer Architecture:** Watch [Karpathy — Let's Build GPT](https://youtu.be/kCc8FmEb1nY) (2hr). Implement `MultiHeadAttention` and `FeedForward` blocks from scratch. Goal: be able to explain every line you wrote.  
**Secondary — HuggingFace intro:** Load GPT-2 with `transformers`. Tokenize text. Run inference. Inspect `model.config`. Understand the `pipeline()` abstraction.  
**Reading:** [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) — Jay Alammar

---

### Week 2
**Primary — Transformer Implementation:** Complete nanoGPT — training loop, cross-entropy loss, sampling with temperature/top-k. Get it training on Shakespeare. Understand why loss goes down.  
**Secondary — HF Model Hub:** Browse HF Hub. Compare GPT-2, Llama 3.1 8B, and Mistral 7B model cards — architecture differences, param counts, context lengths. Load Llama 3.1 8B and run local inference.  
**Reading:** [Attention Is All You Need](https://arxiv.org/abs/1706.03762) — intro + section 3 (architecture). Cross-reference with your nanoGPT implementation.

---

### Week 3
**Primary — Tokenization + Generation Mechanics:** [Karpathy tokenizer video](https://youtu.be/zduSFxRajkE) (first 45 min). Understand BPE at implementation level. Implement temperature, top-p, top-k sampling yourself — understand the math behind each.  
**Secondary — HF Datasets + Tokenizers:** Use `datasets` library to load and preprocess a real dataset. Explore `tokenizers` library internals — fast vs slow tokenizer, special tokens, padding strategies.  
**Reading:** [HuggingFace NLP Course Ch 5–6](https://huggingface.co/learn/nlp-course/chapter5/1) — datasets and tokenization internals

---

### Week 4
**Primary — Alignment: RLHF, DPO, Scaling Laws:** Watch [Nathan Lambert — RLHF series](https://www.youtube.com/@natolambert) (start with "Understanding RLHF" and "DPO explained"). Supplement with [InstructGPT paper](https://arxiv.org/abs/2203.02155) sections 1–3 and [Chinchilla](https://arxiv.org/abs/2203.15556) abstract + conclusion. Nathan's videos are the clearest explainer of the post-training pipeline that exists. You've worked with DPO at Amazon — connect that production experience to the theory here.  
**Secondary — HF PEFT intro:** Read [PEFT docs — LoRA quickstart](https://huggingface.co/docs/peft/quicktour). Run the LoRA example on a small model. Don't go deep yet — get the toolchain working.  
**Reading:** [DPO paper](https://arxiv.org/abs/2305.18290) — you've worked with it in production; now understand the math derivation  
**End of phase:** nanoGPT pushed to GitHub. Can implement and explain every component cold.

---

## Phase 2 — RAG Production Depth + LangGraph Agents Intro (Weeks 5–8)

You've built RAG on Bedrock (Knowledge Bases). Now build it with the open-source stack at production quality — hybrid search, evaluation, observability. In parallel, port your Strands/AgentCore agent experience to LangGraph.

**Active project:** P2 (Production RAG System) — builds across all 4 weeks  
**LeetCode:** Stack & Queue (weeks 5–6) → Binary Search (weeks 7–8) — 5 problems/week  
**ML System Design:** Starts week 5 — chatbot API → semantic search → RAG system → RAG eval pipeline

---

### Week 5
**Primary — Embeddings + Vector Search:** Go deep on what embeddings encode — not just "semantic similarity" but the geometry. Cosine vs dot product vs L2. HNSW indexing. Embed documents with `sentence-transformers`. Store and query in ChromaDB. Compare chunking strategies: fixed-size, sentence-window, semantic.  
**Secondary — LangGraph basics:** Work through [DeepLearning.AI: AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/) lessons 1–3. Build a simple state graph. This is LangGraph ≈ Strands — connect the concepts.  
**Reading:** [Greg Kamradt — chunking strategies](https://github.com/FullStackRetrieval-com/RetrievalTutorials)

---

### Week 6
**Primary — RAG Pipeline (open-source):** Build a full RAG pipeline end-to-end without frameworks first — raw API calls: load → chunk → embed → ChromaDB → retrieve → augment prompt → generate. Then wire it into a FastAPI endpoint with streaming.  
**Secondary — LangGraph agent:** Rebuild your week 6 pipeline as a LangGraph agent. Add Tavily web search as a tool. Add LangSmith tracing. You've done this conceptually with Strands — the mental model transfers.  
**Reading:** [RAGAS paper](https://arxiv.org/abs/2309.15217) — sections 1–3 (the evaluation framework you'll implement next week)

---

### Week 7
**Primary — Hybrid Search + Reranking:** Add BM25 (keyword) + vector (semantic) hybrid search to your P2. Add a Cohere or cross-encoder reranker. Understand *why* hybrid beats either alone. Add Langfuse tracing to every LLM call.  
**Secondary — LangGraph multi-step:** Add memory to your agent (in-context + external ChromaDB). Practice the handoff pattern between nodes. Read [Anthropic: Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — you'll see patterns from your Strands work.  
**Reading:** [RAG paper](https://arxiv.org/abs/2005.11401) (Lewis 2020) — the original; connect to your production work

---

### Week 8
**Primary — RAGAS Evaluation:** Add evaluation harness to P2: 30 Q&A pairs, RAGAS faithfulness + answer relevancy + context recall automated. Add a Streamlit frontend. Write GitHub README with architecture diagram. This is P2 done.  
**Secondary — LangGraph agent polish:** Finish the P3 seed — your research agent with Tavily, LangSmith traces, tool error handling. This becomes Phase 3's starting point.  
**Reading:** [Judging LLM-as-a-Judge](https://arxiv.org/abs/2306.05685) — you've done LLM-as-judge at Amazon; understand the academic framing  
**End of phase:** P2 live on GitHub with RAGAS scores in README and Langfuse dashboard screenshot.

---

## Phase 3 — Agentic AI Deep + Fine-Tuning Toolchain Intro (Weeks 9–12)

Go deep on multi-agent architecture using open-source tools. In parallel, get the fine-tuning toolchain working — you know DPO from Amazon; now learn the modern open-source pipeline (LoRA, QLoRA, Axolotl).

**Active projects:** P3 (Multi-Agent Pipeline) + first QLoRA run (P4 warmup)  
**LeetCode:** Linked Lists (weeks 9–10) → Trees BFS+DFS (weeks 11–12) — **Hard ramp begins: 3 Medium + 2 Hard per week**  
**ML System Design:** Customer support agent → multi-agent assistant → content moderation → code review assistant

---

### Week 9
**Primary — Multi-Agent Architecture:** Build P3 — Supervisor → Planner → Researcher (Tavily) → Writer pipeline in LangGraph. Pass state through the graph. Handle agent handoffs. This is the open-source equivalent of your AgentCore multi-agent work.  
**Secondary — LoRA Theory:** Read [LoRA paper](https://arxiv.org/abs/2106.09685) intro + section 2 (the math). Read [QLoRA paper](https://arxiv.org/abs/2305.14314) intro + section 3. Understand the math before writing training code. You worked with DPO — connect: DPO operates on top of an SFT model, which is what you're about to build.  
**Reading:** [AutoGen paper](https://arxiv.org/abs/2308.08155) — architecture section. Compare to your AgentCore experience.

---

### Week 10
**Primary — Agent Reliability:** Add failure handling to P3 — max retries, bad tool output recovery, fallback paths. Add human-in-the-loop approval for the final output. Add LangSmith traces with per-agent-step spans.  
**Secondary — First LoRA run:** Fine-tune GPT-2 or TinyLlama on a simple task using HF PEFT + LoRA. Goal: get the pipeline working, inspect the adapter weights. Don't optimize.  
**Reading:** [LIMA paper](https://arxiv.org/abs/2305.11206) — data quality > quantity. Relevant to your annotation platform work at Amazon.

---

### Week 11
**Primary — MCP:** Build an MCP server wrapping a real API (GitHub, SQLite, or a domain API of your choice). Connect to Claude Desktop to demo it. Understand why MCP matters — it's the emerging standard for what you've been doing with Bedrock tool use.  
**Secondary — QLoRA environment:** Set up QLoRA on your AWS GPU. Install `bitsandbytes`, load Mistral 7B in 4-bit, verify it runs. Pick your domain dataset for P4 — ideally something adjacent to your Amazon work (ads, classification, preference learning).  
**Reading:** [MCP specification](https://modelcontextprotocol.io/introduction) + [Simon Willison's explainer](https://simonwillison.net/2024/Nov/25/model-context-protocol/)

---

### Week 12
**Primary — P3 Polish:** Clean README, architecture diagram, LangSmith trace screenshots, demo recording. P3 done.  
**Secondary — Fine-tuning prep:** Format your chosen domain dataset in Alpaca instruction format. Configure Axolotl for QLoRA. Run a short training sanity check (1 epoch, few hundred examples) — just verify the loss decreases.  
**Reading:** [Axolotl README](https://github.com/axolotl-ai-cloud/axolotl) — config options  
**End of phase:** P3 live on GitHub. QLoRA environment working. Domain dataset ready.

---

## Phase 4 — Fine-Tuning Deep + Eval + Observability (Weeks 13–16)

Full QLoRA fine-tune end-to-end. Eval and observability run in parallel because you need them to measure whether fine-tuning is working. You've done LLM-as-judge and annotation quality work at Amazon — this phase will feel familiar conceptually, with new tooling.

**Active projects:** P4 (fine-tuned model) + eval harness on P2  
**LeetCode:** Graphs (weeks 13–14) → DP 1D+2D (weeks 15–16) — **continue Hard: 3 Medium + 2 Hard per week**  
**ML System Design:** Fine-tuning pipeline → recommendation system with LLMs → LLM serving infra → prompt management + A/B testing

---

### Week 13
**Primary — QLoRA Fine-Tune Run:** Full training run with Axolotl — iterate on dataset quality, LR, rank. Log with W&B. Run at least 2 configurations. Connect to your annotation platform experience: data quality is the same problem.  
**Secondary — Eval Harness:** Build eval harness for P2 — 50 Q&A pairs, RAGAS faithfulness + relevancy automated, script runs on every code change. Connect to your LLM-as-judge work at Amazon.  
**Reading:** [Axolotl config docs](https://github.com/axolotl-ai-cloud/axolotl) — fine-tuning configuration options

---

### Week 14
**Primary — Before/After Benchmark:** Run your P4 benchmark — 20 test prompts, base vs fine-tuned scored with LLM-as-judge. Prepare HuggingFace model card. Push adapter to HF Hub. This is your "depth below the API layer" proof.  
**Secondary — DPO + Post-Training deep dive:** Watch [Nathan Lambert — DPO deep dive + reward modeling](https://www.youtube.com/@natolambert) videos. Run [TRL DPO trainer](https://huggingface.co/docs/trl/dpo_trainer) on a small preference dataset. You've implemented DPO at Amazon — now understand the full post-training pipeline (SFT → reward model → RL or DPO) in the open-source stack.  
**Reading:** [DPO paper](https://arxiv.org/abs/2305.18290) sections 3–4 — the full derivation. Also: Nathan Lambert's [Interconnects newsletter](https://www.interconnects.ai/) — the best ongoing coverage of post-training research.

---

### Week 15
**Primary — Observability:** Add Langfuse tracing to P3 (multi-agent pipeline) — per-agent-step spans, token cost, latency. Set up prompt versioning. This is the open-source equivalent of whatever internal observability you use at Amazon.  
**Secondary — promptfoo:** Add `promptfoo` automated test cases to P2. Configure regression detection — alert when faithfulness drops below threshold. Write the eval script that runs on every prompt change.  
**Reading:** [Langfuse docs — prompt management](https://langfuse.com/docs/prompts/get-started)

---

### Week 16
**Primary — P4 Polish:** Clean README with benchmark results table, training config, before/after examples. Model card on HF Hub. P4 done.  
**Secondary — LLM-as-Judge depth:** Re-read [Judging LLM-as-a-Judge](https://arxiv.org/abs/2306.05685) — specifically the failure modes and biases. You use this at Amazon; now be able to critique it in an interview.  
**Reading:** [W&B prompts guide](https://docs.wandb.ai/guides/prompts/) — experiment tracking for LLM systems  
**End of phase:** P4 on HuggingFace Hub. Full eval harness on P2. All 4 projects exist and are functional.

---

## Phase 5 — Production Serving + Interview Sprint (Weeks 17–20)

No new projects. Deploy what exists. From week 19 the primary focus shifts entirely to interview prep.

**LeetCode:** Heap + Priority Queue (weeks 17–18) → timed mock sessions Hard/Medium mix (weeks 19–20)  
**ML System Design:** Real-time writing assistant → multimodal Q&A → mock interview × 2

---

### Week 17
**Primary — vLLM + Inference Optimization:** Serve your P4 model with vLLM. Benchmark throughput vs naive HF inference — actually observe the numbers. Understand PagedAttention and continuous batching not just conceptually but by watching the GPU utilization.  
**Secondary — Interview Prep begins:** Start the conceptual Q&A list in the README. One topic per session — explain out loud, record yourself, watch it back.  
**Reading:** [PagedAttention paper](https://arxiv.org/abs/2309.06180) abstract + section 2. [Tim Dettmers on quantization](https://timdettmers.com/2022/08/17/llm-int8-and-emergent-features/).

---

### Week 18
**Primary — Production Deployment:** Dockerize P2 (FastAPI + ChromaDB + Langfuse). Add LiteLLM as a proxy layer. Deploy to Modal Labs or HuggingFace Spaces. Record demo GIFs for all 4 project READMEs.  
**Secondary — Interview Prep:** Work through system design questions. Write up your answers as documents in `log/`. Practice talking through them — 10 minutes max per design.  
**Reading:** [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — know the list for security questions

---

### Week 19
**Primary — Interview Prep:** System design mock sessions — timed, structured, no notes. RAG at scale, agent with HITL, eval pipeline design, LLM serving infra. Find a peer or use Claude to critique your designs.  
**Secondary — GitHub polish:** All 4 repos: clean READMEs, architecture diagrams, live demo links, pinned on profile. Update LinkedIn with projects. Write 1 LinkedIn post about P2 or P3.  
**Reading:** Nothing new — review all 5 topic files, fill any conceptual gaps you find.

---

### Week 20
**Primary — Interview Prep:** Coding exercises under time pressure — implement attention from scratch, implement ReAct loop, implement basic RAG pipeline, streaming FastAPI endpoint. These are the actual coding tasks.  
**Secondary — Applications:** Send applications if you haven't already. Tailor resume to each company's language (Google: scale + research; Meta: systems + experimentation; Anthropic: alignment + model internals; Apple: privacy + on-device; Netflix: personalization + A/B).  
**Deliverable:** Interview-ready. All 4 projects live. Applications sent.
