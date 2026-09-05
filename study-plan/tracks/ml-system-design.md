# ML System Design Track

**Target:** 1 design problem per week, starting week 5 (once you have enough context to reason about systems).  
**Format:** 45–60 min per problem. Write up your design in `log/` or `projects/`. Then review against the framework below.

---

## Design Framework (use for every problem)

Work through these sections in order — same structure every time builds interview muscle memory.

```
1. Clarify requirements (5 min)
   - Scale: how many users, requests/sec, data volume?
   - Latency: real-time vs batch?
   - Quality: accuracy vs cost vs speed tradeoff?

2. High-level architecture (10 min)
   - Draw the boxes: data sources → processing → model → serving → clients
   - Identify the critical path

3. Data layer (10 min)
   - What data do you need? Where does it come from?
   - How do you store it? (vector DB, relational, blob)
   - How do you handle updates?

4. Model / LLM layer (10 min)
   - What model? Fine-tuned vs API vs open-source?
   - RAG vs fine-tuning vs prompting — justify the choice
   - How do you version it?

5. Serving layer (10 min)
   - Sync vs async? Streaming?
   - How do you handle load? Caching strategy?
   - Latency budget per component

6. Evaluation + monitoring (5 min)
   - How do you measure quality in production?
   - What metrics do you alert on?
   - How do you detect regression?
```

---

## Problem Progression (weeks 5–19)

Start simple, increase complexity and scale each week. Condensed by one week versus a naive schedule (14 problems + 2 mock weeks = 16 weeks) — the two mock sessions are combined into a single week 19 alongside the LeetCode mock week.

| Week | Problem | Key Skills It Tests |
|------|---------|---------------------|
| 5 | Design a conversational chatbot API | API design, context management, streaming |
| 6 | Design a semantic document search system | Embeddings, vector DB, indexing at scale |
| 7 | Design a RAG system for a 10M-document corpus | Chunking strategy, hybrid search, scaling retrieval — draw on Phase 1's dual/cross-encoder work |
| 8 | Design a RAG evaluation pipeline | Eval metrics, regression detection, human feedback loop |
| 9 | Design a customer support agent | Agent architecture, escalation, safety, HITL |
| 10 | Design a multi-agent research assistant | Orchestration, parallelism, failure recovery |
| 11 | Design a content moderation pipeline | LLM + classifier combo, latency vs accuracy, appeals |
| 12 | Design a code review assistant | Tool use, context window management, structured output |
| 13 | Design a fine-tuning pipeline for a domain model | Data curation, training infra, eval, rollback |
| 14 | Design a recommendation system with LLMs | Embedding retrieval + reranking + personalization |
| 15 | Design an LLM serving infrastructure (vLLM scale) | Throughput, batching, autoscaling, cost |
| 16 | Design a prompt management + A/B testing system | Versioning, experimentation, rollout strategy |
| 17 | Design a real-time AI writing assistant | Streaming, low latency, caching |
| 18 | Design a multimodal document Q&A system | Vision + text, chunking PDFs/images |
| 19 | Mock design interview ×2 (pick any from above) | Timed, no notes, structured response |

---

## Resources

- **Chip Huyen — [Designing ML Systems](https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/)** (book) — the standard reference
- **[Full Stack Deep Learning](https://fullstackdeeplearning.com/)** — free lectures on deployment + system design
- **[ByteByteGo](https://bytebytego.com/)** — general system design patterns (useful for the infra layer)
- **[ML System Design Interview (Educative)](https://www.educative.io/courses/machine-learning-system-design)** — structured interview prep

---

## Common Failure Points in ML System Design Interviews

- **Jumping to the model before clarifying requirements** — always start with requirements
- **Ignoring the data layer** — data quality + freshness is usually the bottleneck, not the model
- **Not justifying RAG vs fine-tuning vs prompting** — interviewers specifically probe this tradeoff
- **Skipping evaluation** — every design needs a clear answer to "how do you know it's working?"
- **No failure handling** — what happens when the LLM API is down? When retrieval returns garbage?
