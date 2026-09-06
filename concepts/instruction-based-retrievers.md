# Instruction-Based Retrievers: Promptriever and Rank1

## One-line summary
Standard retrievers only ask "is this about the same topic as the query?" — instruction-based retrievers also honor natural-language constraints beyond topicality (style, sentiment, exclusion conditions). Promptriever bakes this into a dual-encoder; Rank1 bakes it into a cross-encoder/reranker via distilled reasoning traces. Both from the same JHU group (Orion Weller et al.), a natural bi-encoder/cross-encoder pairing.

## How it works

**The problem:** a query like "find documents about data privacy, but written using extended metaphors" has a topical part (data privacy) and an instruction part (a stylistic constraint). Keyword search and standard semantic similarity both only see the topical part — the instruction gets silently dropped.

**[Promptriever](https://arxiv.org/abs/2409.11136) (bi-encoder / dual-encoder, Sept 2024):** the first dense retrieval model that can be prompted like an LM. Trained with **instruction negatives** — documents that are relevant to the query's *topic* but violate the specific *instruction* — which forces the embedding to actually encode the instruction, not just topical similarity. Trained on ~500k instance-level instructions curated from MS MARCO. This is the same dual-encoder architecture already in the plan (see week 1-2), just with a training objective that adds instruction-following on top of topical relevance.

**[Rank1](https://arxiv.org/abs/2502.18418) (cross-encoder/reranker, COLM 2025):** the first reranker trained to use test-time compute. Distills 600k+ reasoning traces from a large reasoning model (R1-style) on MS MARCO queries/passages, so the reranker produces an explicit step-by-step chain-of-thought about relevance *before* scoring — explainable, and works well out-of-distribution. This is the same cross-encoder role already in the plan (week 3/5's reranker), with reasoning-model distillation added.

## Intuition / mental model
This is the instruction-following layer on top of the dual-encoder/cross-encoder split you're already building: Promptriever = "teach the fast first-stage retriever to notice constraints, not just topics"; Rank1 = "teach the slow, accurate reranker to reason explicitly about whether a document actually satisfies the query, constraints included." Same architectural roles, new training objective.

## When it's used
Any retrieval task where relevance means more than topical similarity — style/tone requirements, exclusion criteria ("about X but not Y"), logical conditions, domain-specific relevance definitions that a generic embedding model was never trained to distinguish.

## Evaluation
**FollowIR** and **InstructIR** are the standard benchmarks here — evaluation suites for instruction-following retrieval, not models themselves. Promptriever reports gains on both (+14.3 p-MRR / +3.1 nDCG on FollowIR, +12.9 Robustness on InstructIR) — see [[ranking-metrics-mrr-ndcg]] for what those metrics mean.

## Related
- [[bright-benchmark]] — Rank1's primary evaluation benchmark, and the sharpest example of "relevance beyond topicality"
- [[ranking-metrics-mrr-ndcg]], [[traditional-vs-rag-era-retrieval-eval]]
- [Rank-K: Test-Time Reasoning for Listwise Reranking](https://arxiv.org/pdf/2505.14432) (May 2025) — a distinct, later paper in the same reasoning-reranking lineage as Rank1, already flagged in `tracks/research-paper.md`'s landscape scan
- Source: Benjamin Clavié — [P3: Optimizing Retrieval with Reasoning Models](https://hamel.dev/notes/llm/rag/p3_reasoning.html)
