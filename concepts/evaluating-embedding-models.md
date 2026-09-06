# Evaluating Embedding Models (MTEB and generalization)

## One-line summary
When comparing embedding models on a benchmark like MTEB, weight out-of-domain/niche-domain task performance more heavily than the aggregate average — it's a better signal of real generalization than overall leaderboard rank.

## How it works
MTEB (Massive Text Embedding Benchmark) aggregates many tasks and datasets across domains — retrieval, classification, clustering, and more — into a single leaderboard score. A model can top the aggregate by being very strong on common, well-represented domains (often ones close to its own training data) while being mediocre on unusual or niche domains. The average hides this — two models with the same overall score can have very different generalization profiles.

## Intuition / mental model
Like a GPA across very different classes: a model that aces the "easy," data-adjacent tasks and does just okay elsewhere can out-rank a model that's more consistently good across unfamiliar territory. For a production retrieval system, the real corpus almost never looks exactly like MTEB's common tasks — so the niche/out-of-domain subscore is the more honest predictor of how a model will actually perform on your data.

## When it's used
- Choosing an embedding model for a domain-specific retrieval system (e.g. comparing E5 / BGE / OpenAI / Voyage for a specific corpus — see [[dual-encoder-retrieval]] once that note exists, and `study-plan/week-by-week.md` week 2)
- Any time a benchmark aggregates diverse tasks into one score — "don't trust the average, check the tails" generalizes past MTEB

## Related
- Source: Benjamin Clavié — [P2: Modern IR Evals For RAG](https://hamel.dev/notes/llm/rag/p2-evals.html)
- [[ranking-metrics-mrr-ndcg]] — the actual metrics MTEB's retrieval tasks report (mostly NDCG@k)
- [[bright-benchmark]] — the starkest version of this lesson: the same top MTEB model scores 59.0 nDCG@10 on MTEB, 18.3 on BRIGHT
- [[multi-vector-retrieval]] (once that note exists)
