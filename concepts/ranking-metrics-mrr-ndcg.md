# Ranking Metrics: MRR and NDCG

## One-line summary
MRR scores how quickly you hit the *first* relevant result; NDCG scores the quality of the *whole* ranked list, discounted by position, and handles graded (not just binary) relevance.

## How it works

**MRR (Mean Reciprocal Rank)**
- For a single query: reciprocal rank = `1 / rank of the first relevant result` (e.g. first relevant doc at position 3 → 1/3)
- MRR = average of reciprocal ranks across all queries
- Range: 0–1, higher is better
- Only looks at the *first* relevant hit — ignores whether there are more relevant docs further down, and ignores their positions entirely

**NDCG (Normalized Discounted Cumulative Gain)**
- DCG = sum over the ranked list of `relevance_score / log2(rank + 1)` — relevant docs count, but a logarithmic discount means lower-ranked ones contribute less
- IDCG = DCG of the *ideal* ranking (all docs sorted by true relevance, best first)
- NDCG = `DCG / IDCG` — normalizes to 0–1, so it's comparable across queries even when they have different numbers of relevant docs
- Usually computed as NDCG@k (e.g. NDCG@10) — only the top-k results count
- Supports *graded* relevance (e.g. 0/1/2/3, not just relevant/not-relevant) — this is the key thing MRR can't do

## Intuition / mental model
MRR asks "how far did I have to scroll to find *an* answer?" — it's a single-answer metric, blind to everything except the first hit. NDCG asks "how good is my whole top-k list, weighted so results near the top matter more?" — it's the right metric when multiple results can be relevant to different degrees (e.g. a search result that's "somewhat relevant" vs "exactly what I wanted").

## When it's used
- **MRR:** good fit when there's typically one right answer (e.g. "find the one document that answers this question," QA-style retrieval)
- **NDCG:** good fit for general ranked search/recommendation where multiple results can be relevant with different degrees of quality — this is what most retrieval benchmarks (including MTEB's retrieval tasks) actually report
- Both predate LLM-based eval (RAGAS, LLM-as-judge) — they measure ranking quality directly from relevance judgments, not generation quality. Use them for the retrieval stage; use RAGAS/LLM-as-judge for the generation stage on top of retrieval. See `study-plan/topics/02-building-with-llms.md` and week 6's eval harness work.

## Related
- [[evaluating-embedding-models]] — MTEB reports NDCG for most of its retrieval tasks
- Source: Benjamin Clavié — [P2: Modern IR Evals For RAG](https://hamel.dev/notes/llm/rag/p2-evals.html)
