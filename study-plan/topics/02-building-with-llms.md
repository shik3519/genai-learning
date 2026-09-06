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
- **Generative retrieval:** a different paradigm entirely — instead of searching an index, a seq2seq model directly generates a document identifier for a query (e.g. DSI and successors). No separate index/ANN search step; retrieval *is* generation. Interesting for its different failure modes (struggles with corpus updates — the identifiers are baked into the model's weights) and as a bridge concept between retrieval and generation. Landscape-level understanding is enough here — see the [GenIR survey](https://arxiv.org/abs/2404.14851) (TOIS 2025) for the full taxonomy across sparse/dense/cross-encoder/late-interaction/generative/hybrid.
- **Choosing for a latency/accuracy budget:** typical production pipeline is dual-encoder (or hybrid dense+sparse) for first-stage retrieval over the full corpus → cross-encoder or late-interaction reranking over a small top-k. Know how to justify this pipeline shape and what changes at different scale/latency constraints — this is the kind of question that comes up directly in retrieval-systems interviews.

### RAG Pipelines
- **RAG architecture:** load → chunk → embed → index → retrieve → augment prompt → generate
- **Retrieval quality:** precision vs recall tradeoff; top-k selection; contextual compression
- **RAGAS metrics:** faithfulness, answer relevancy, context recall — the eval standard
- **Failure modes:** hallucination when retrieved context is wrong; chunk boundary issues

## The Resources

**DeepLearning.AI — [Building Systems with the ChatGPT API](https://www.deeplearning.ai/short-courses/building-systems-with-chatgpt/)** (free, 2hr)  
Covers APIs, tool use, and RAG end to end. Practical and fast.

**Hamel Husain — [Stop Saying RAG Is Dead](https://hamel.dev/notes/llm/rag/not_dead.html)** (7-post series)  
Directly relevant to this phase's retrieval-SOTA arc: argues the future of RAG is better retrieval, not bigger context windows, and covers exactly the things this plan is building toward — late-interaction (ColBERT) preserving token-level detail, reasoning-enabled retrievers, why naive single-vector search loses information, "context rot" (performance degradation with longer inputs), and evaluation that measures coverage/diversity rather than naive IR metrics. Read alongside week 5-6's SOTA/eval work.

**For APIs specifically:** [Anthropic API docs — tool use](https://docs.anthropic.com/en/docs/build-with-claude/tool-use) — the authoritative reference.

## Must-Read Papers

- [RAGAS](https://arxiv.org/abs/2309.15217) — the standard for evaluating RAG systems; read sections 1–3
- [ColBERT](https://arxiv.org/abs/2004.12832) — late-interaction retrieval; intro + architecture
- [SPLADE](https://arxiv.org/abs/2107.05720) — learned sparse retrieval; abstract + section 2
- [From Matching to Generation: A Survey on Generative IR](https://arxiv.org/abs/2404.14851) (TOIS 2025) — the full retrieval landscape taxonomy; read this first (week 1) before the individual architecture deep-dives below

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
