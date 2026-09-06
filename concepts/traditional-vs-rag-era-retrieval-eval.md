# Traditional Search Eval vs RAG-Era Eval

## One-line summary
Traditional IR eval (MRR, NDCG, Precision/Recall@k) asks "did we rank the relevant document(s) highly?" against fixed relevance judgments; RAG-era eval has to additionally ask "did retrieval give the LLM *enough, and diverse enough* material to synthesize a faithful, complete answer?" — a different task shape, not just a different metric.

## How it works

**Traditional search:** query → ranked list of documents → scored against relevance judgments (qrels) using MRR, NDCG, Precision@k, Recall@k (see [[ranking-metrics-mrr-ndcg]]). Implicit assumptions: each document is independently relevant or not (or gradedly so), the goal is surfacing the best one(s) as high as possible, and a human reads down the list themselves.

**RAG:** query → retrieved chunks → fed to an LLM → generated answer. This breaks the traditional assumptions in a few ways:
- **Completeness/coverage, not just rank:** a single top-1 chunk can score perfectly on MRR/NDCG while still being *insufficient* — if the real answer requires synthesizing across 3 chunks and only 1 was retrieved, ranking metrics don't catch the gap. RAGAS's **context recall** targets this directly.
- **Diversity, not just relevance:** for open-ended or multi-faceted queries, retrieving 5 near-duplicate high-scoring chunks can rank well but still fail to cover the question — this is Clavié's coverage/diversity critique of naive single-vector RAG eval.
- **Downstream generation quality enters the loop:** even with perfect retrieval, the LLM can still hallucinate or miss the point — **faithfulness** (is the answer grounded in what was retrieved, not invented) and **answer relevancy** (does the answer address the question) measure the generation stage, which traditional IR eval never had to account for since there was no generation stage.

## Intuition / mental model
Traditional search is a librarian pointing you to the single best book. RAG is a librarian handing a stack of pages to someone else, who then has to write a report from them — it's not enough that the top page is great; the report-writer needs *everything relevant*, without irrelevant noise drowning it out. Ranking the single best page perfectly is necessary but not sufficient.

## When it's used
- **MRR/NDCG-style ranking eval:** good for the retriever *in isolation* (sanity-check: is the embedding/reranking model surfacing the right things at all?), and for genuine "find the single best match" use cases (e.g. a single-answer QA lookup)
- **RAGAS/coverage/diversity + faithfulness/answer-relevancy:** needed for the *end-to-end* RAG pipeline, especially multi-hop or synthesis-heavy queries where no single chunk is "the answer"
- In practice: use both, at different layers. Ranking metrics catch a broken retriever early and cheaply; end-to-end RAGAS/LLM-as-judge catches whether the full pipeline actually produces a good answer. One passing doesn't guarantee the other.

## Related
- [[ranking-metrics-mrr-ndcg]]
- [[evaluating-embedding-models]]
- Source: synthesized from Benjamin Clavié's ["Stop Saying RAG Is Dead"](https://hamel.dev/notes/llm/rag/not_dead.html) series (P2: Modern IR Evals For RAG) + `study-plan/topics/02-building-with-llms.md`'s existing RAGAS coverage
