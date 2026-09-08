# Research Paper Track

**Target:** Submit to KDD (or an equivalent applied-ML venue), deadline ~February 2027.
**Format:** Milestone-based, not weekly-uniform like LeetCode. Runs underneath the main phases — don't let it silently slip because a phase is busier some week.

---

## Why this shape

Unlike LeetCode or ML System Design, a paper doesn't decompose into equal weekly units — topic selection, experiments, and writing have different rhythms and can't be reordered. This track is a sequence of milestones with rough week ranges, not a fixed weekly assignment.

## Candidate Topic Angles (decide by end of Phase 1, ~week 6–7)

Two live candidates, evaluate both during Phase 1 as the relevant skills come online:

1. **Retrieval-angle:** something grounded in the Amazon retrieval-systems project — e.g., a comparison or a novel combination of dual-encoder / cross-encoder / late-interaction retrieval under a specific constraint (latency, domain shift, cold-start). Phase 1's weeks 1–6 (dual-encoder → cross-encoder → hybrid → ColBERT/SPLADE) are direct groundwork for scoping this.
2. **RL-angle:** something from the Phase 2 PPO/DPO/GRPO-from-scratch comparison — e.g., a systematic empirical comparison of the three on a specific task class, or applying GRPO-style reasoning RL to a retrieval or agentic task (a natural hybrid of both candidate angles).
3. **A specific, well-scoped variant of the retrieval-angle — controlled fine-tuned comparison:** see [[finetuned-dual-encoder-vs-late-interaction]] in `concepts/`. There's surprisingly thin evidence comparing a fine-tuned dual-encoder against a fine-tuned late-interaction model *with the same backbone and training data* — most published comparisons differ on backbone/training too, conflating architecture with everything else. A rigorous controlled study on your own domain data (using `pylate`) doesn't need a novel algorithm — the methodology itself is the contribution, which fits KDD's applied track well and is genuinely more tractable than the hybrid/RL angles below.

A hybrid of the two original angles (RL-optimized retrieval/reranking — e.g., preference-tuned rerankers, RL for query rewriting) is worth explicitly considering; it uses both new skill investments and ties directly to the day job.

**Decision criteria:** what's the novel angle (not just "applying X to Y"), what data/compute do you actually have access to (Amazon compute helps here), and what's achievable to a submittable standard by ~week 16.

## Landscape scan (as of September 2026)

A quick tier-1-venue sweep of the last ~1-2 years, to sanity-check the candidate angles against where academia actually is right now:

- **RAG + RL/reasoning fusion is hot at NeurIPS 2025** — "Chain-of-Retrieval Augmented Generation" (o1-style step-by-step retrieve-and-reason), "Improving RAG through Multi-Agent Reinforcement Learning," "DynamicRAG" (LLM-feedback-driven dynamic reranking). This validates the **hybrid angle** (RL-optimized retrieval/reranking) as a real, active area — good news for feasibility, but it also means the bar for genuine novelty there is higher than it looked a few months ago.
- **Close precedents exist — read these early, during the survey milestone:** [Promptriever](https://arxiv.org/abs/2409.11136) (instruction-trained dual-encoder) and [Rank1](https://arxiv.org/abs/2502.18418) (reasoning-trace-distilled reranker) — both from the same JHU group, both directly in the "teach retrieval to do more than topical matching" space the hybrid angle would occupy — plus [Rank-K: Test-Time Reasoning for Listwise Reranking](https://arxiv.org/pdf/2505.14432) (2025), a later, distinct paper in the same lineage. See [[instruction-based-retrievers]] in `concepts/`. If the hybrid angle is chosen, the paper needs to clearly differentiate from all three, not just replicate the general idea of "add reasoning to retrieval."
- **Efficient/lightweight reranking is a strong, more narrowly-scoped SIGIR/EMNLP/ECIR 2025 theme** — "MICE: Minimal Interaction Cross-Encoders," "PLAID" (efficient late-interaction serving), "Efficient Re-ranking via Early Exit," block-level embedding approaches. A dedicated ECIR 2026 workshop on late-interaction/multi-vector retrieval confirms this is still very active. This is a **more scoped, lower-competition variant of the retrieval-angle** worth weighing against the broader hybrid angle — efficiency-under-constraint framings (latency budget, memory budget) tend to be easier to make a clean novelty claim around than "combine X and Y."
- **GRPO successors are proliferating fast** (DAPO, GSPO, GFPO, CISPO, per Nathan Lambert's [rlhfbook.com](https://rlhfbook.com/) and ICML/ICLR 2025 papers) — if the pure **RL-angle** (PPO vs DPO vs GRPO comparison) is chosen, position it carefully: a from-scratch pedagogical comparison is valuable, but claiming it as *novel* research is a harder sell given how fast this specific sub-area is moving. The hybrid or retrieval-efficiency framings currently look like better bets for a genuine novelty claim within the plan's constraints.
- **Practitioner sentiment matches the venue trend:** Benjamin Clavié's ["Stop Saying RAG Is Dead" series](https://hamel.dev/notes/llm/rag/not_dead.html) (industry, not a venue paper, but widely read) makes the same case from the applied side — specifically [P3: Optimizing Retrieval with Reasoning Models](https://hamel.dev/notes/llm/rag/p3_reasoning.html) is the practitioner-side companion to the Rank-K paper above, and [P2: Modern IR Evals For RAG](https://hamel.dev/notes/llm/rag/p2-evals.html)'s eval critique (coverage/diversity, not just RAGAS-style metrics) is directly relevant to whatever evaluation section the paper ends up needing. Worth reading both during the survey milestone.
- **A concrete benchmark-construction methodology worth reusing:** [FreshStack](https://arxiv.org/abs/2504.13128) (NeurIPS 2025, Datasets and Benchmarks track — see [[freshstack-benchmark-creation]] in `concepts/`) mines real Stack Overflow Q&A into atomic "nugget" facts, then pools multiple retrievers to build nugget-level relevance judgments, specifically to fight benchmark contamination and coarse whole-document judgments. Whichever paper angle gets chosen, this is a strong template for the paper's own evaluation methodology — a domain-specific, nugget-level eval set is a much stronger reviewer-facing artifact than generic Q&A pairs, and the "resist contamination via freshness" framing is itself citable as prior art for the eval design.

**Working recommendation given this scan:** the field now has three reasonably distinct options, roughly in order of tractability-vs-ambition: (1) the **controlled fine-tuned dual-encoder vs late-interaction comparison** — most tractable, thin existing evidence, no novel algorithm required; (2) **retrieval-efficiency or hybrid RL+retrieval** — more ambitious, more crowded, higher novelty bar; (3) a **pure RL-algorithm comparison** — least likely to read as novel given how fast GRPO successors are moving. Lean toward (1) as the safer core, with room to fold in (2)'s framing (e.g. efficiency-under-constraint) if the controlled comparison alone feels too narrow once results are in. Revisit at the week 6–7 topic-lock milestone once Phase 1's retrieval work and Phase 2's RL work are both further along.

## Milestones

| Milestone | Target week | Notes |
|---|---|---|
| Survey + informal lit review of both candidate angles | 1–6 | Runs alongside Phase 1's retrieval work; don't formally commit yet |
| Topic locked | ~6–7 | Write a 1-page internal problem statement: question, hypothesis, novelty claim, evaluation plan |
| Related work review (formal) | 7–9 | Overlaps Phase 2 if RL-angle; can run in parallel with Phase 1 wrap-up if retrieval-angle |
| Experiment pipeline built | 9–12 | Minimal working pipeline, not yet the full experiment matrix |
| Core experiments | 12–16 | Overlaps Phase 3/4 — budget real time here, this is usually the slowest part |
| First full draft | 16–17 | Get something end-to-end even if rough — forces you to find the gaps |
| Writing, figures, related work polish | 17–19 | Overlaps interview sprint (Phase 5) — this is the known crunch point |
| Internal review + revision | 19–20 | Ask a peer or use Claude for a structured review pass |
| Submit | ~Feb 2027 | Buffer week(s) before the actual deadline for camera-ready-quality polish |

## Logging

Note paper progress in the weekly `log/` entry under a dedicated line — even "no progress this week, Phase 3 crunch" is useful signal for the weekly check-in to catch drift early, since this track has no automatic weekly cadence to fall back on.

## Paper craft

The plan is heavy on the ML content (retrieval, RL) but writing a competitive empirical paper is its own skill — framing novelty against related work, choosing baselines, ablation design, anticipating reviewer objections. You've published 7 papers so this isn't new, but it's worth a deliberate refresher rather than assuming it'll take care of itself under deadline pressure: Simon Peyton Jones' ["How to Write a Great Research Paper"](https://www.microsoft.com/en-us/research/academic-program/write-great-research-paper/) is the standard reference, ~1 hour, worth revisiting once the topic is locked (~week 6-7).

## Fallback: workshop submission

If a full draft isn't real by week 16-17 (the milestone table's own checkpoint), don't let the full KDD research-track deadline become a slow-motion miss. Pivot deliberately to a workshop paper instead — lower length/novelty bar, and workshops attached to KDD or adjacent venues (IR, GenAI, agents-focused) often have later or rolling deadlines. Naming this now means it's a planned decision made at week 16, not a scramble in week 19. Revisit this explicitly at the week 16-17 milestone regardless of how things are going — don't wait for it to become obviously necessary.

## Risk

The known conflict is weeks 17–19: paper writing and interview-sprint prep overlap. Per the plan's earlier decision, the **job search timeline is protected** — if the two genuinely conflict in a given week, the interview sprint (mocks, applications, system design) takes the time and paper work flexes: compress the writing pass, or push polish/submission-buffer past week 19 into February rather than cutting into interview prep. Flag it in `log/` when this happens so `status.md` reflects the real trade-off, not the original plan.
