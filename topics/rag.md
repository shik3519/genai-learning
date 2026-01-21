# RAG (Retrieval-Augmented Generation)

## TL;DR
RAG combines a retriever (to fetch relevant context) with a generator (LLM) so the model can answer questions using external knowledge instead of only its parameters.

## Intuition
- Use the LLM mainly as a **reasoning and synthesis engine**, not a database.
- If the model doesn’t “know” something, fetch it from a knowledge source on demand.
- Good retrieval + good prompts can often beat naive fine-tuning for knowledge-heavy tasks.

## Core Concepts
- Document chunking and preprocessing.
- Embeddings and vector stores for similarity search.
- Retrieval strategies (k, filters, hybrid).
- Prompt construction from retrieved context.

## Simple Example
- Problem: Q&A over product docs.
- Pipeline:
  - Ingest + chunk docs.
  - Embed and index chunks.
  - At query time: embed question, retrieve top-k chunks.
  - Build prompt: instructions + question + retrieved chunks.
  - Call LLM and return answer.

## Gotchas & Common Pitfalls
- Too-large chunks → context bloat, irrelevant text.
- Too-small chunks → lost semantics.
- Over-reliance on LLM without checking retrieval quality.
- Forgetting to evaluate end-to-end task performance.

## Connections
- Related topics:
  - [[llm-basics]]
  - [[agents-and-tools]]
- Related projects:
  - [[mini-rag-bot]]

## References / Resources
- Paper / blog:
- Notes:
