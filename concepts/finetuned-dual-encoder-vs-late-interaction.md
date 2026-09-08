# Fine-Tuned Dual-Encoder vs Fine-Tuned Late-Interaction: A Thin Evidence Base

## One-line summary
When both a single-vector (dual-encoder) and a multi-vector (late-interaction) model are fine-tuned on the *same* in-domain data with the *same* backbone, the late-interaction model still significantly outperforms — but this kind of controlled, apples-to-apples comparison is rare in the literature. Most published comparisons pit off-the-shelf models with different backbones/training against each other, which conflates architecture with everything else that differs.

## How it works
In the P4 Q&A, Antoine Chaffin (ModernBERT/PyLate co-creator) was asked directly: does the single-vector vs multi-vector performance gap persist once both are fine-tuned on identical in-domain data? His answer: yes — pointing to the BRIGHT benchmark, where a late-interaction model significantly outperformed a single-vector model *with the same backbone and training data*. So the mechanism itself (multiple vectors + late interaction vs one compressed vector) appears to be doing real work, not just "whichever model happened to be trained better."

The gap: this is one Q&A answer citing one comparison, not a systematic study. Most of the field's evidence for "late-interaction beats dense" comes from comparing different off-the-shelf models (different backbones, different pretraining, different fine-tuning recipes) — which can't cleanly separate "the interaction mechanism helps" from "this particular model happened to be trained better."

## Intuition / mental model
This is the difference between correlation and an isolated, controlled comparison. "Late-interaction models tend to score higher on leaderboards" is weak evidence for "late-interaction is architecturally better" if the models being compared differ in ten other ways too. A genuine controlled study — same backbone, same data, only the interaction mechanism varies — is what actually answers the architectural question, and there's not much of it.

## When it's relevant
- **Directly actionable for P2 and the Amazon retrieval work:** fine-tuning both a dual-encoder and a late-interaction model (e.g. via `pylate`) on the same domain-specific data would produce a genuinely useful, under-covered data point — not just a portfolio comparison table, a real controlled result.
- **A concretely scoped candidate for the research paper:** this doesn't require inventing a new algorithm — careful, controlled methodology *is* the contribution, which is exactly the kind of empirical/benchmark-track paper KDD's applied track rewards. Worth weighing against the other candidate angles in `tracks/research-paper.md`, or using as supporting evidence within whichever angle is chosen.

## Related
- [[modern-late-interaction-models]] — PyLate is the practical tool to actually run this fine-tuned comparison
- [[bright-benchmark]] — where the cited comparison happened
- Source: Benjamin Clavié / Antoine Chaffin Q&A — [P4: Late Interaction Models For RAG](https://hamel.dev/notes/llm/rag/p4_late_interaction.html)
