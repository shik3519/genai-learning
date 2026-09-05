# CLAUDE.md

Orientation for any Claude session (interactive or the scheduled weekly routine) working in this repo.

## What this repo is

Shikhar's personal GenAI/LLM learning log and study tracker. It exists to serve three goals at once:

1. **Job switch** — targeting Applied Scientist roles (Google, Meta, Anthropic, Apple, Netflix) with a mix of research depth and production/deployment ability. See `study-plan/README.md`.
2. **Deepen expertise domain** — production LLM/agent systems (Bedrock, RAG, prompt engineering, multi-agent), building on real production experience.
3. **Learn new skills** — close specific gaps: transformer internals at implementation depth, the open-source stack (HuggingFace, LangGraph, PEFT, vLLM, Langfuse), and LeetCode/ML system design at interview bar.

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

- **`study-plan/README.md`** — the plan overview: target, timeline, 3 pillars, 5 phases, 4 portfolio projects. Changes rarely.
- **`study-plan/week-by-week.md`** — the detailed 3-6 month roadmap (currently a 20-week plan), broken into phases and weeks with primary/secondary focus. This is the **source of what to study, in what order** — but it's a living plan, not a contract. It's fine to reorder, skip, or extend phases as real progress and priorities shift.
- **`study-plan/status.md`** — the **living source of truth for where things actually stand**: current week/phase, what's completed, what's actively in flight, where he's stuck, confidence levels per topic. This is the file that should always reflect reality, not the plan.
- **`study-plan/topics/`** — reference notes per GenAI topic (foundations, building with LLMs, agentic AI, fine-tuning, eval/production).
- **`study-plan/tracks/`** — standing tracks that run every week regardless of phase: `leetcode.md`, `ml-system-design.md`.

## Two standing workflows

### "What should I study next?"

1. Read `study-plan/status.md` for current week, what's done, what's stuck, confidence levels.
2. Cross-reference `study-plan/week-by-week.md` for that week/phase's primary + secondary focus, and the standing tracks (`tracks/leetcode.md`, `tracks/ml-system-design.md`).
3. Check the last 1-2 `log/` entries for anything flagged as unresolved or "still fuzzy."
4. Give a concrete, scoped recommendation for the session/week — not a re-statement of the whole plan. If he's behind on something from last week, say so and fold it in rather than silently advancing the calendar.

### Logging progress

When told what was studied/built in a session:

1. Create or update today's `log/YYYY-MM-DD.md` from `templates/log.md`.
2. Update `study-plan/status.md`: current week, "what's completed," "actively working on," "where stuck," and confidence levels if they changed.
3. Don't over-engineer this — a few honest lines beat exhaustive notes.

## Weekly scheduled check-in

A cloud routine runs weekly (Sunday evening, America/Los_Angeles) to keep `status.md`'s "current week" focus fresh even between conversations. It follows the same "what should I study next" logic above, and commits the update directly to `status.md`. It carries work forward if the prior week wasn't finished rather than mechanically advancing the week counter — the plan adapts to actual progress, not the calendar.
