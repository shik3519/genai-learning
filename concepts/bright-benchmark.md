# BRIGHT Benchmark

## One-line summary
BRIGHT is a retrieval benchmark where relevance requires genuine reasoning, not topic matching — e.g. finding a math problem that uses the *same theorem*, or a coding problem solved with the *same algorithm*, even when the surface topic is completely different. State-of-the-art embedding models collapse on it: MTEB's leading model scores 59.0 nDCG@10 on MTEB but only 18.3 on BRIGHT.

## How it works
1,384 real-world queries across diverse domains (economics, psychology, math, coding). The defining property: relevance is defined by "unique relevance definitions that go beyond topic matching" — a relevant document might share no vocabulary or topic with the query at all, only the same underlying concept or method. Clavié's example: given a LeetCode problem, the relevant match is another problem solvable with the same two-pointer approach, regardless of what the problems are ostensibly "about."

Chain-of-thought query augmentation (having an LLM reason about the query before retrieving) improves scores by up to 12.2 points — direct evidence that the missing ingredient is reasoning, not better embeddings.

## Intuition / mental model
Standard retrieval benchmarks ask "find documents about the same thing." BRIGHT asks "find documents that require the same underlying reasoning to solve/understand," which a dual-encoder trained on topical/semantic similarity has no mechanism to see — the surface form can be unrelated. It's the retrieval-eval equivalent of an analogy test rather than a keyword-matching test.

## When it's used
- The standard evaluation benchmark for reasoning-based retrievers/rerankers — it's [[instruction-based-retrievers|Rank1's]] primary eval set.
- A sharp, concrete illustration of the [[evaluating-embedding-models|MTEB generalization lesson]]: the *same* top-ranked MTEB model drops from 59.0 to 18.3 nDCG@10 on BRIGHT. If a retrieval task looks anything like "same underlying reasoning, different surface topic," MTEB rank alone tells you almost nothing.

## Related
- [[instruction-based-retrievers]] — BRIGHT is Rank1's eval benchmark
- [[evaluating-embedding-models]] — the MTEB-vs-BRIGHT score gap is the sharpest version of "don't trust the aggregate"
- [[ranking-metrics-mrr-ndcg]] — BRIGHT is scored with nDCG@10
- Paper: [BRIGHT: A Realistic and Challenging Benchmark for Reasoning-Intensive Retrieval](https://arxiv.org/abs/2407.12883)
- Source: Benjamin Clavié — [P3: Optimizing Retrieval with Reasoning Models](https://hamel.dev/notes/llm/rag/p3_reasoning.html)
