# Review of *Prism: Training Small Language Models for Agentic Pipeline Replacement via RLVR and Knowledge Distillation*

## Summary

---

## Quality

### Strengths

Strengths: The experimental design is internally coherent: the same reward function (Equation 2) drives both the RLVR gradient signal and the KD trace filter, avoiding the common pitfall of optimizing inconsistent objectives across training stages. The KD-50 vs KD-100 contrast is methodologically valuable. Many KD papers report a single dataset size; the jump from +0.020 to +0.620 across a 2× data scaling is interesting observation.

Weaknesses: The evaluation is severely underpowered. With 10 held-out tasks across 4 categories, most cells have $n \in \{2, 3\}$. A single task flipping changes the bug-fix score by ~0.33 in absolute terms. No confidence intervals, seeds, or significance tests are reported. No baselines beyond the base model. Missing are: Zero-shot prompting of a comparably-sized open model, Vanilla SFT on raw teacher traces (no reward filtering) — the critical baseline for the "re-scoring matters" claim, Few-shot ICL on Llama-3.1-8B itself. Single model family, single teacher, single seedL The paper studies only Llama-3.1-8B with GPT-4o as teacher. The "complementarity" claim is structural and defended by exactly one (student, teacher, dataset) configuration. The KD-50 → KD-100 discontinuity is unexplainedL:The paper observes the phase change (40 vs. 80 post-filter traces) but offers no analysis of why it occurs at that threshold — coverage across categories, a per-category minimum, optimization dynamics? A learning curve at intermediate values (60, 70, 80, 90 tasks) would have transformed an observation into a mechanism.

---

## Clarity

Strengths: The paper is well-organized and easy to follow.

Weakness: The benchmark is underspecified. There is no example task, no example reward predicate, no description of input length, and no explanation of how multi-file tasks are encoded into a single-step correction problem.

---

## Originality

**Strengths:** The specific framing — replacing individual pipeline nodes rather than training a general-purpose assistant, and demonstrating complementary failure modes of RLVR and KD on that task type — is, to my knowledge, not standard in the literature. The unified reward abstraction across KD and RLVR is a small but genuine design contribution.

**Weakness:** The proposed KD → RLVR sequential recipe is never tested. The paper argues for it from the failure-mode analysis but does not run the combined experiment — the central practical recommendation is motivated, not validated. The individual technical components are also not novel: GRPO is from DeepSeekMath; rejection-sampled SFT is standard (RFT, R1's cold-start, STaR-family). The contribution lies in the packaging and the empirical contrast, not in any new training algorithm.

---

## Significance

If the headline numbers hold up at scale, the work has clear practical relevance. The cost asymmetry between frontier APIs and self-hosted 8B models is real and growing, and many production agentic systems are exactly the high-volume, narrow-task pipelines where node replacement is economically viable.

---

## Pros and Cons

### Pros

- Coherent two-method framework with a shared reward abstraction that connects RLVR and KD cleanly.
- Informative failure-mode analysis — RLVR collapses on sparse rewards while KD needs trace volume; the contrast is a clean experimental finding.
- Cost-motivated framing (Equation 1) gives the work a clear practical target audience.

### Cons

- Severely underpowered evaluation — 10 held-out tasks is too few to support the claims.
- No critical baselines: vanilla SFT without reward filtering, prompted Llama-3.1-8B, or few-shot ICL.
- The proposed KD → RLVR recipe is never empirically tested despite being the paper's central practical recommendation.
- The KD-50 → KD-100 phase change is observed but not analyzed; no intermediate learning curve is provided. No intuition on why this is observed
