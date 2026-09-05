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

A hybrid of the two (RL-optimized retrieval/reranking — e.g., preference-tuned rerankers, RL for query rewriting) is worth explicitly considering; it uses both new skill investments and ties directly to the day job.

**Decision criteria:** what's the novel angle (not just "applying X to Y"), what data/compute do you actually have access to (Amazon compute helps here), and what's achievable to a submittable standard by ~week 16.

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

## Risk

The known conflict is weeks 17–19: paper writing and interview-sprint prep overlap. Per the plan's earlier decision, the **job search timeline is protected** — if the two genuinely conflict in a given week, the interview sprint (mocks, applications, system design) takes the time and paper work flexes: compress the writing pass, or push polish/submission-buffer past week 19 into February rather than cutting into interview prep. Flag it in `log/` when this happens so `status.md` reflects the real trade-off, not the original plan.
