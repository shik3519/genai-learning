# Topic 2: Building with LLMs — APIs, RAG & Embeddings

## Core Concepts

### APIs & Prompting
- **Chat completions:** system/user/assistant roles — how the conversation loop works
- **Structured outputs:** JSON mode, tool schemas, `instructor` library — forcing typed responses
- **Tool use / function calling:** how the model decides to call a function vs respond directly
- **Streaming:** why it matters for UX; how to handle streamed chunks in FastAPI
- **Prompt engineering:** few-shot, Chain-of-Thought, ReAct — when each helps
- **Cost & token counting:** estimating cost before a call; prompt caching (Anthropic)

### Embeddings & Vector Search
- **Embeddings:** dense vectors encoding semantic meaning; cosine vs dot product similarity
- **Chunking:** fixed-size, sentence-window, semantic — tradeoffs for retrieval quality
- **Vector databases:** indexing (HNSW), approximate nearest neighbor; ChromaDB, FAISS, Weaviate
- **Hybrid search:** BM25 (keyword) + vector (semantic) + reranking — better than either alone

### Retrieval Architectures — Dual-Encoder vs Cross-Encoder vs SOTA (interview-favorite, directly relevant to production retrieval work)
- **Dual-encoder (bi-encoder):** query and document each encoded independently by the same (or a paired) tower; similarity is a single dot product/cosine at query time. Cheap — documents are pre-encoded, retrieval is ANN search. This is what "embeddings + vector DB" means architecturally.
  - Trained with contrastive loss: in-batch negatives, hard negative mining matter a lot for quality.
- **Cross-encoder:** query and document concatenated and encoded *together* through full attention, single relevance score out — architecturally just a transformer encoder with a classification head. Much more accurate (sees query-doc interaction directly) but can't be precomputed — too slow for first-stage retrieval over a large corpus. Used as a **reranker** over a dual-encoder's top-k.
- **Late-interaction (ColBERT/ColBERTv2):** middle ground — encode query and doc into *multiple* token-level vectors (not one), compute similarity via a cheap max-sim aggregation at query time. Nearly cross-encoder accuracy at closer-to-dual-encoder speed, at the cost of much more storage (per-token vectors, not one vector/doc).
- **Learned sparse (SPLADE):** learns sparse, interpretable term-weight vectors (extending BM25's idea with a learned model) — combines some of dense retrieval's quality with sparse retrieval's efficient inverted-index infrastructure.
- **Generative retrieval:** a different paradigm entirely — instead of searching an index, a seq2seq model directly generates a document identifier for a query (e.g. DSI and successors). No separate index/ANN search step; retrieval *is* generation. Interesting for its different failure modes (struggles with corpus updates — the identifiers are baked into the model's weights) and as a bridge concept between retrieval and generation. Landscape-level understanding is enough here — see the [GenIR survey](https://arxiv.org/abs/2404.14851) (TOIS 2025) for the full taxonomy of this specific paradigm; it's not a good general retrieval-landscape resource (see below), it's specifically deep on generative retrieval.
- **Multimodal retrieval (landscape-level):** the dual-encoder idea generalizes across modalities — CLIP trains an image tower and a text tower with the same contrastive, in-batch-negative objective as a text-only dual-encoder, so similarity search works across text↔image. This stays conceptual for this plan (broader multimodal work is out of scope per the plan's cuts), but it's worth knowing the architecture is the same idea you're already implementing, just paired towers over different modalities.
- **Choosing for a latency/accuracy budget:** typical production pipeline is dual-encoder (or hybrid dense+sparse) for first-stage retrieval over the full corpus → cross-encoder or late-interaction reranking over a small top-k. Know how to justify this pipeline shape and what changes at different scale/latency constraints — this is the kind of question that comes up directly in retrieval-systems interviews.

### RAG Pipelines
- **RAG architecture:** load → chunk → embed → index → retrieve → augment prompt → generate
- **Retrieval quality:** precision vs recall tradeoff; top-k selection; contextual compression
- **RAGAS metrics:** faithfulness, answer relevancy, context recall — the eval standard
- **Failure modes:** hallucination when retrieved context is wrong; chunk boundary issues

## The Resources

**DeepLearning.AI — [Building Systems with the ChatGPT API](https://www.deeplearning.ai/short-courses/building-systems-with-chatgpt/)** (free, 2hr)  
Covers APIs, tool use, and RAG end to end. Practical and fast.

**Benjamin Clavié — ["Stop Saying RAG Is Dead" series](https://hamel.dev/notes/llm/rag/not_dead.html)** (7 parts, hosted as notes on Hamel Husain's site) — **the primary retrieval-landscape resource for this phase**, established approaches first, not generative-retrieval-heavy:
- [P1: I don't use RAG, I just retrieve documents](https://hamel.dev/notes/llm/rag/p1-intro.html) — intro/landscape (week 1)
- [P2: Modern IR Evals For RAG](https://hamel.dev/notes/llm/rag/p2-evals.html) — eval beyond RAGAS-style single-answer metrics (week 6)
- [P3: Optimizing Retrieval with Reasoning Models](https://hamel.dev/notes/llm/rag/p3_reasoning.html) — reasoning-based retrieval, bridges to Phase 2/the paper (week 6)
- [P4: Late Interaction Models For RAG](https://hamel.dev/notes/llm/rag/p4_late_interaction.html) — ColBERT/late-interaction, the accessible entry point before the paper (week 5)
- [P5: RAG with Multiple Representations](https://hamel.dev/notes/llm/rag/p5_map.html) — multi-representation/hybrid (week 4)
- [P6: Context Rot](https://hamel.dev/notes/llm/rag/p6-context_rot.html) — performance degradation with longer inputs; optional, connects to Phase 5's serving work
- [P7: You Don't Need a Graph DB (Probably)](https://hamel.dev/notes/llm/rag/p7-graph-db.html) — graph-like retrieval without graph infra; optional, not scheduled

**For APIs specifically:** [Anthropic API docs — tool use](https://docs.anthropic.com/en/docs/build-with-claude/tool-use) — the authoritative reference.

## Must-Read Papers

- [RAGAS](https://arxiv.org/abs/2309.15217) — the standard for evaluating RAG systems; read sections 1–3
- [ColBERT](https://arxiv.org/abs/2004.12832) — late-interaction retrieval; intro + architecture
- [SPLADE](https://arxiv.org/abs/2107.05720) — learned sparse retrieval; abstract + section 2
- [CLIP](https://arxiv.org/abs/2103.00020) — cross-modal dual-encoder; abstract + architecture (multimodal retrieval, landscape-level)
- [From Matching to Generation: A Survey on Generative IR](https://arxiv.org/abs/2404.14851) (TOIS 2025) — optional, deep dive specifically on generative retrieval (not a general landscape survey — use the Clavié series above for that)

## Key Libraries

| Library | Use |
|---------|-----|
| `anthropic` | Anthropic API client |
| `instructor` | Structured outputs from any LLM |
| `chromadb` | Local vector database |
| `sentence-transformers` | Embedding models |
| `ragas` | RAG evaluation |
| `langfuse` | Tracing + observability |
| `fastapi` | API serving |

## Project

**P2 — Production RAG System** — see [week-by-week.md](../week-by-week.md) weeks 1–6 (Phase 1, secondary track).

## Interview Questions

1. What is RAG and when would you use it over fine-tuning?
2. How do you choose chunk size for a RAG system?
3. What is hybrid search and why is it better than vector-only search?
4. Dual-encoder vs cross-encoder — architecture and tradeoffs? Where does late-interaction (ColBERT) sit between them, and at what cost?
5. What does "faithfulness" mean in RAGAS? How do you measure it?
6. How does function calling work — what does the model actually output?
7. How would you reduce hallucination in a RAG system?
8. What is prompt caching and how does it reduce cost?
9. Design a RAG system for a 10M document corpus. What changes at that scale?
