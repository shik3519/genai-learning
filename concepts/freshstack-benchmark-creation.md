# FreshStack: How to Build a RAG Benchmark

## One-line summary
FreshStack (NeurIPS 2025) builds retrieval/RAG benchmarks by mining real Stack Overflow Q&A into atomic "nuggets" of required facts, then pooling multiple retrievers against real GitHub technical docs to find supporting evidence per nugget — giving fine-grained, contamination-resistant relevance judgments instead of static whole-document labels.

## How it works
Three steps:
1. **Automatic corpus collection** — pull code and technical documentation from GitHub repositories (real, current material, not a curated academic corpus).
2. **Nugget generation** — take a real Stack Overflow question + answer pair, feed it to GPT-4o to extract "nuggets": short, atomic facts that are actually necessary to answer the question.
3. **Nugget-level support** — for each nugget, retrieve supporting documents using a *fusion of multiple retrieval techniques* (hybrid architectures), pooling their results together to build the relevance judgments. Evaluation then happens at the nugget level, not the whole-document level.

## Intuition / mental model
Traditional benchmarks ask "is document D relevant to query Q?" — coarse, whole-document, binary-ish. FreshStack instead asks "does this specific atomic fact, needed to fully answer Q, show up somewhere in what was retrieved?" — this is a concrete, implementable version of the **coverage** problem described in [[traditional-vs-rag-era-retrieval-eval]]: a system can nail the single best-ranked document (great MRR/NDCG) while still missing nuggets 2 and 3 of a 3-part answer. Nugget-level judgment catches that; whole-document judgment doesn't.

The other deliberate design choice: **built to be continuously refreshed with recent topics**, specifically to fight benchmark contamination — once a static benchmark is public, later models absorb it into pretraining and start "memorizing" the right answers rather than genuinely retrieving/generalizing. Sourcing from recent Stack Overflow activity is a direct countermeasure.

## When it's used
- **Directly actionable for P2's eval harness (week 6) and the paper's evaluation section**: the methodology — mine real user questions relevant to your domain, extract atomic facts an answer needs, pool multiple retrieval methods to build judgments — is a reusable recipe, not just a fixed dataset. Worth borrowing the *process* even without using FreshStack's own data, especially since a domain-specific eval set (vs. generic RAGAS Q&A pairs) is more convincing both in a portfolio README and in a paper.
- Whenever evaluating a RAG system that needs to synthesize across multiple facts/chunks (most real systems), not just retrieve one relevant document.

## Related
- [[traditional-vs-rag-era-retrieval-eval]] — nugget-level judgment is a concrete implementation of the coverage idea
- [[ranking-metrics-mrr-ndcg]]
- Paper: [FreshStack: Building Realistic Benchmarks for Evaluating Retrieval on Technical Documents](https://arxiv.org/abs/2504.13128) (NeurIPS 2025, Datasets and Benchmarks track)
- Source: Benjamin Clavié — [P2: Modern IR Evals For RAG](https://hamel.dev/notes/llm/rag/p2-evals.html)
