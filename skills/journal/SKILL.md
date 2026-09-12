---
name: journal
description: Capture an end-of-session reflection to the user's personal journal at ~/.claude/journal/ — how the user and the agent actually worked together, not a technical recap of what was built. The trigger is divergence: reflect when the agent's direction differed from the user's and was argued out, when multiple options were weighed, when the plan turned out to be wrong (a re-cut, a superseded decision, work redone), when the user's workflow itself changed, or when they voice reduced confidence in the output or process. Skip a session that was pure execution against an agreed plan, however long or generative it looked. Use when the user says "wrap up", "journal this session", "reflect on this session", "/journal", or similar — and offer proactively, citing the specific divergence observed, when the session is ending and one occurred.
---

# Journal

Build a long-term record of *how* the user iterates with Claude — their reactions, preferences, and friction — so future sessions start oriented instead of cold.

This is **not** a technical recap, and it does not duplicate auto-memory. Auto-memory stores conclusions: one fact, one rule, one preference. The journal stores the *argument* — the paths weighed, why the user's differed from the agent's, what the plan got wrong. That doesn't compress into a rule without losing the part worth keeping.

## When to reflect

The trigger is **divergence**. Reflect when the session contained any of:

- the agent proposed a direction, the user disagreed, and it was argued out
- multiple options were genuinely weighed before one was chosen
- the plan turned out to be wrong — a re-cut, a reversed decision, work redone, a premise that didn't hold
- the user changed how they work (different tooling, different model split, a step they normally take was skipped), or commented on the workflow itself
- the user expressed reduced confidence in the output, the codebase, or the process

Any one of these is enough. The second and third are the highest-signal: a plan that bent tells you more about how the work really goes than a plan that held.

## When not to

Skip a session that was **pure execution against an agreed plan** — code written, tests passing, no disagreement — no matter how long, technical, or productive it was. Nothing was learned about how the user works, and an entry that records nothing surprising dilutes the ones that do. Empty calories hurt the signal.

Session length, session kind, and how much got built are all irrelevant to this decision. Only divergence matters.

## Invoking

**Explicit triggers** — run immediately, don't ask:

- "wrap up", "journal this session", "reflect on this session", "save a reflection", "/journal"

**Proactive offer** — when the session is ending (the user says "we're done", "let's stop here", "I'll come back tomorrow", or runs `/compact`) **and** a divergence occurred, offer once, **naming the evidence**:

> "We re-cut once and reversed the storage decision — worth a reflection?"

Citing the specific divergence is what makes the offer worth reading. A generic "want me to journal this?" is noise; the user can't tell whether you noticed something real. If no divergence occurred, stay silent — don't ask. If the answer is no, drop it and don't ask again this session.

## Drafting

Read `~/.claude/journal/README.md` before drafting — that file is the source of truth for the template and folder layout. If it has diverged from this skill, follow it.

**First run:** if it doesn't exist, the journal isn't set up. Create `~/.claude/journal/reflections/` and `~/.claude/journal/distilled/`, copy `assets/journal-README.md` to `~/.claude/journal/README.md`, and say you've done so. The user owns that file from then on.

What goes in:

- **The divergence itself** — what was proposed, what the user wanted instead, and why. The reasoning on both sides, not just the outcome.
- **How the user iterated** — did they open broad and narrow? Add requirements mid-stream? Lock decisions via structured questions or direct correction?
- **Reactions** — what they liked, pushed back on, and especially **what they silently accepted**. Silent confirmations are the highest-signal entries because the user never volunteers them.
- **Keep / Change** — concrete behaviours to repeat or stop, specific enough that another Claude reading this in six months could act on it.
- **Open threads** — unresolved tensions and follow-ups.

What stays out: a summary of what was built (that's in the code, the PR, or the shape log), the technology choices themselves unless the user reacted to them, and praise for either party. If the draft reads like a status update, cut the technical content and re-focus on the collaboration.

## Length and tone

Match `assets/reflection-example.md`, or the user's own recent reflections once a few exist. Candid, specific, short sentences, bullets over prose. Named patterns ("structured questions in batches of 3–4") over vague impressions ("communication was good"). Aim for 250–500 words; longer only if there were genuinely several notable patterns.

## Ritual

1. **Decide** whether a divergence occurred. If unsure, ask once, naming what you think you saw.
2. **Choose a filename** — `YYYY-MM-DD-<short-slug>.md` in `~/.claude/journal/reflections/`, slug 2–4 lowercase hyphenated words. If that file exists, append `-2`.
3. **Draft** from signals actually in the conversation. Don't invent reactions the user didn't have.
4. **Show the draft in chat first.** Never save before showing.
5. **Save** after the user confirms or edits.
6. **Check for a repeat** — compare this reflection's **Change** entries against earlier ones. A restated lesson is the promotion signal; act on it this session, don't queue it.
7. **Offer distillation** only when the conditions below are met.

## Promotion — the delivery half

A reflection nobody reads changes nothing. Capture is half the loop; promotion is what makes a lesson act on a future session, because reflections are never loaded into context and skills and auto-memory always are.

When a **Change** entry repeats one from an earlier reflection, promote it the same session. Ranked by durability:

1. **Into a skill** — planning lessons to `plan-kickoff`, execution-cadence lessons to `shape-dd`. A rule there fires every time the skill triggers. Both skills carry a **Local calibration** section: person-specific values and preferences belong there, not in the general rules. That separation is what keeps a skill shareable while still absorbing what it learns.
2. **Into auto-memory** as a `feedback` entry — for lessons that cut across phases.
3. **Left in the journal** — fine for anything not yet clearly recurring, but it will influence nothing until promoted.

Never promote without explicit confirmation. Always *raise* it: a third occurrence of the same Change entry is a defect in the loop, not another data point.

## Distillation

After saving, offer to synthesise when **either** 5+ reflections are newer than `~/.claude/journal/distilled/preferences.md`, **or** 30 days have passed since it was last modified and at least one reflection is newer. (If it doesn't exist: 5+ reflections total.) A fixed count alone would disable distillation whenever the journal goes quiet — which is exactly when the gap is worth examining.

If yes: read every reflection newer than the current `preferences.md`, and write ~30–60 short categorised bullets — **Iteration patterns**, **What works**, **What to avoid**, **Open tensions**. No narrative, pure rules. Overwrite; distilled files are derivative.

## Edge cases

- **Empty or brand-new session** — nothing to reflect on. Say so and stop.
- **The conversation was compacted** — work from current context and flag that earlier signal may have been lost.
- **A reflection on a previous session** — you don't have that context. Offer to write one from what the user remembers, in their words.
- **30+ days since the last reflection** — say so and ask one question: what changed in between? A quiet journal usually means the work moved somewhere the trigger doesn't fire, and that answer is worth more than the current entry.
- **Multiple sessions in one day** — append `-2`, `-3`, or merge if the topics are continuous and the user prefers.
- **The user wants it private / not promoted** — fine. The journal is theirs; never auto-promote to auto-memory without confirmation.
