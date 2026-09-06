# CLAUDE.md

Orientation for any Claude session (interactive or the scheduled weekly routine) working in this repo.

## What this repo is

Shikhar's personal GenAI/LLM learning log and study tracker. It exists to serve four goals at once:

1. **Job switch** — targeting Applied Scientist roles (Google, Meta, Anthropic, Apple, Netflix) with a mix of research depth and production/deployment ability. See `study-plan/README.md`.
2. **Deepen expertise domain** — push past what the day job (a retrieval-systems project at Amazon) requires: retrieval SOTA (dual-encoder, cross-encoder, late-interaction/ColBERT, SPLADE) and post-training/RL implemented from scratch (PPO, DPO, GRPO), not just used.
3. **Learn new skills** — close specific gaps: transformer internals at implementation depth, the open-source stack (HuggingFace, LangGraph, PEFT, vLLM, Langfuse), LeetCode/ML system design at interview bar, and becoming a genuine power user of agentic coding tools.
4. **Research paper** — submit to KDD (or an equivalent venue), deadline ~February 2027. Likely angle: bridging the Amazon retrieval work with the RL/post-training depth being built in Phase 2. See `study-plan/tracks/research-paper.md`.

He has access to larger internal Amazon compute for small-scale projects — worth using for the RL and fine-tuning phases when local-GPU scale is limiting.

## Repo map

```
CLAUDE.md          — this file
log/                — dated study-session entries (what was covered, what's next)
concepts/           — evergreen notes, one file per concept
projects/           — one folder per project, notes + code together
study-plan/         — the study plan and progress tracker (see below)
templates/          — starters for log/concept/project notes
scratch.md          — quick capture: links, half-formed thoughts, todos
```

## study-plan/ — the tracking system

- **`study-plan/README.md`** — the plan overview: target, timeline, goals, pillars, 5 phases, 4 portfolio projects. Changes rarely.
- **`study-plan/week-by-week.md`** — the detailed 3-6 month roadmap (currently 19 weeks), broken into phases and weeks with primary/secondary focus. This is the **source of what to study, in what order** — but it's a living plan, not a contract. It's fine to reorder, skip, or extend phases as real progress and priorities shift.
- **`study-plan/status.md`** — the **living source of truth for where things actually stand**: current week/phase, what's completed, what's actively in flight, where he's stuck, confidence levels per topic. This is the file that should always reflect reality, not the plan.
- **`study-plan/topics/`** — reference notes per GenAI topic (foundations, building with LLMs + retrieval SOTA, agentic AI, fine-tuning, eval/production, post-training/RL).
- **`study-plan/tracks/`** — standing tracks: `leetcode.md`, `ml-system-design.md` (weekly cadence), `agentic-coding.md` (ongoing, light), `research-paper.md` (milestone-based, not weekly).

## Three standing workflows

### "What should I study next?"

1. Read `study-plan/status.md` for current week, what's done, what's stuck, confidence levels.
2. Cross-reference `study-plan/week-by-week.md` for that week/phase's primary + secondary focus, and the standing tracks (`tracks/leetcode.md`, `tracks/ml-system-design.md`, `tracks/agentic-coding.md`).
3. Check `study-plan/tracks/research-paper.md` for the current milestone — it doesn't have a weekly slot, so it's easy to silently drop; flag it if it looks stale.
4. Check the last 1-2 `log/` entries for anything flagged as unresolved or "still fuzzy," **and their "Time spent" totals.**
5. **Load check:** if logged hours have run past ~20/week for 2+ weeks running, say so explicitly and propose a concrete scope cut (drop a project's polish bar, compress the paper's current milestone, etc.) rather than just handing over the next chunk of the plan as if nothing's wrong. Update `status.md`'s "Load check" section when this happens. See `study-plan/README.md`'s "Honest Load Check" for the reasoning and the two safeguards this plan is built with.
6. Give a concrete, scoped recommendation for the session/week — not a re-statement of the whole plan. If he's behind on something from last week, say so and fold it in rather than silently advancing the calendar.

### Logging progress

When told what was studied/built in a session:

1. Create or update today's `log/YYYY-MM-DD.md` from `templates/log.md`, including the "Time spent" section — don't skip it, it's the input to the load check above.
2. Update `study-plan/status.md`: current week, "what's completed," "actively working on," "where stuck," and confidence levels if they changed.
3. Don't over-engineer this — a few honest lines beat exhaustive notes.

### Filing resource notes

When told something learned from a resource (a paper, video, book chapter, talk — pasted highlights, a summary, or just a raw half-formed thought), file it into `concepts/` without asking him to format or categorize it first:

1. Decide whether it fits an existing `concepts/*.md` file or needs a new one — one file per concept, using `templates/concept.md`'s structure (one-line summary, how it works, intuition, when it's used, code sketch, related). Don't force every section if there's not enough material yet; a partial file beats a padded one.
2. Link related concepts with `[[wikilink]]` (existing convention — this is an Obsidian vault).
3. Say where it went (new file vs. appended to an existing one) so he can find it later — never file it silently.
4. This is separate from `log/` (dated, "what I did this session") and `status.md` (plan tracking) — concept notes are evergreen, not tied to a date or a week number.

## Weekly scheduled check-in

A cloud routine runs weekly (Sunday evening, America/Los_Angeles) to keep `status.md`'s "current week" focus fresh even between conversations. It follows the same "what should I study next" logic above, and commits the update directly to `status.md`. It carries work forward if the prior week wasn't finished rather than mechanically advancing the week counter — the plan adapts to actual progress, not the calendar.
