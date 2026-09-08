# Retrieval Method Comparison (P2)

## Goal
- Hands-on implementation of every major retrieval approach on real data — not just reading papers — to build genuine, defensible understanding of the tradeoffs.
- Produce blog-worthy artifacts incrementally, one per stage, not one giant write-up at the end.
- Lay direct groundwork for the research paper's candidate angle 3 — see [[finetuned-dual-encoder-vs-late-interaction]] and `study-plan/tracks/research-paper.md`.

This supersedes the old "RAG over my own notes" framing — same project slot, sharper goal, now tied to the study plan's Phase 1 secondary track (weeks 2–6).

---

## Stage 1 — Baseline comparison harness (weeks 2–4)

**Dataset:** [SciFact](https://github.com/allenai/scifact) via the `beir` library (`BeIR/scifact` on HF) — ~5,183 documents, ~300 queries, real graded relevance judgments (qrels). Small enough to run entirely on a laptop, standard enough that your numbers are sanity-checkable against published leaderboards. (Alternative if you want a harder case: NFCorpus — medical/nutrition domain, informal queries vs. formal doc language, known to stress dense-vs-lexical differences more.)

**Methods to implement, in this order (matches weeks 2–5 of the plan):**
1. **BM25** (sparse baseline) — `rank_bm25` or Pyserini. Trivial to stand up; this is your floor.
2. **Dual-encoder** — `sentence-transformers` (start with something small like `bge-small-en` or `all-MiniLM-L6-v2`), indexed in ChromaDB. Reuses your week 2 infra directly.
3. **Cross-encoder reranker** — rerank the dual-encoder's top-50 with `cross-encoder/ms-marco-MiniLM-L-6-v2`. Week 3.
4. **Late-interaction** — `pylate` + a small ColBERT-style model (or GTE-ModernColBERT if compute allows). Week 5, per [[modern-late-interaction-models]].
5. **Hybrid** — BM25 + dual-encoder fusion (reciprocal rank fusion is the simplest correct starting point). Week 4.

**Metrics:** NDCG@10, Recall@10, MRR (see [[ranking-metrics-mrr-ndcg]]) via the `ranx` library — same tool PyLate uses, so this harness stays consistent across methods. Also log **latency per query** and **index size on disk** for each method — the accuracy/latency/storage tradeoff table is the single most useful artifact this stage produces, and it's exactly what `topics/02-building-with-llms.md`'s "choosing for a latency/accuracy budget" section asks you to be able to defend in an interview.

**Deliverable:** one table (method × NDCG@10 × Recall@10 × MRR × p50 latency × index size) + a short write-up of what surprised you. **This is Blog Post 1.**

---

## Stage 2 — Build your own domain-specific eval set (weeks 5–6)

Generic benchmarks like SciFact don't prove anything about *your* domain. Build a small one yourself, FreshStack-style (see [[freshstack-benchmark-creation]]):

1. Pick a real technical domain you know — a specific library's docs + real GitHub issues or Stack Overflow questions about it (avoid anything Amazon-proprietary; pick a public project).
2. Mine ~30–50 real questions. For each, extract the atomic "nugget" facts a correct answer needs (an LLM can help here, same as FreshStack used GPT-4o).
3. Pool your Stage 1 methods to find supporting documents per nugget, building nugget-level relevance judgments instead of coarse whole-document ones.
4. Rerun the exact Stage 1 harness on this new dataset.

**The question this answers:** does the ranking of "which method wins" change between the generic benchmark and your own domain-specific one? This is the MTEB-vs-BRIGHT generalization lesson (see [[evaluating-embedding-models]], [[bright-benchmark]]) tested at your own small scale, with your own hands.

**Deliverable:** a second comparison table + a write-up on what changed and why. **This is Blog Post 2** — genuinely novel content, since you built the dataset yourself.

---

## Stage 3 — Fine-tuned comparison (paper extension, after Phase 2)

Fine-tune **both** a dual-encoder and a late-interaction model (via `pylate`) on Stage 2's domain data, same backbone where possible. Test whether the late-interaction advantage survives controlled fine-tuning — the exact open question in [[finetuned-dual-encoder-vs-late-interaction]].

This is deliberately sequenced *after* Phase 2 (weeks 7–9), once PPO/DPO/GRPO implementation is done and you have more fine-tuning fluency, and it's the experimental core of the paper's candidate angle 3 if that's the one chosen at the week 6–7 topic lock. Don't start this stage early — Stages 1–2 need to be solid first, and starting a fine-tuning run before the topic is locked risks wasted compute on the wrong comparison.

---

## What I Learned
<!-- Fill in as you go, per stage -->

## Links
- Related concepts: [[evaluating-embedding-models]], [[ranking-metrics-mrr-ndcg]], [[traditional-vs-rag-era-retrieval-eval]], [[freshstack-benchmark-creation]], [[instruction-based-retrievers]], [[bright-benchmark]], [[modern-late-interaction-models]], [[finetuned-dual-encoder-vs-late-interaction]]
- Research paper: `study-plan/tracks/research-paper.md`
- Code: (add repo/path once started)
