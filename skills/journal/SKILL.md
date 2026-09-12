---
name: journal
description: Capture an end-of-session reflection to the user's personal journal at ~/.claude/journal/ — focused on the user's reactions, preferences, and iteration cadence, NOT a technical recap of what was built. Most valuable for *generative* sessions like planning, architecting features, discussing ideas, exploring trade-offs, or running the shape-dd skill. Generally NOT useful for debugging, code review, mechanical refactors, or other reactive sessions where few preferences surface — with one exception: reflect regardless of session kind when work had to be redone (a plan superseded, an implementation refactored soon after landing), when the user's workflow itself changed, or when they express reduced confidence in the process or codebase. Use when the user says "wrap up", "journal this session", "reflect on this session", "/journal", or anything similar. Also use proactively (with permission) when the user signals the session is ending — e.g. they run /compact, say "we're done", "let's stop here", "good place to stop", "I'll come back tomorrow" — AND the session involved planning, architecting, shaping, or open-ended discussion. The point is to capture preferences and friction before context is lost; skip it at a generative session boundary and that signal is gone forever.
---

# Journal

Build a long-term, narrative record of *how* the user iterates with Claude — their reactions, preferences, friction points, and silent confirmations — so future sessions feel smoother from the start. This is **not** a technical recap. It complements (does not replace) the auto-memory system: memory holds atomic action-shaping rules; the journal holds the story behind them.

## When this skill is valuable (and when it isn't)

The signal-to-noise ratio depends heavily on the *kind* of session. Reflect generously on generative work; be stingy on reactive work.

**High-value sessions (reflect by default if a trigger fires):**
- Planning, architecting, designing new features
- Open-ended discussion, brainstorming, exploring trade-offs
- Distilling a fuzzy intent into a plan or spec
- Sessions using the `shape-dd` skill (intent → shape → slice review is exactly the kind of iteration this journal exists to capture)
- Re-scoping, prioritising, or making a multi-way decision between approaches

**Low-value sessions (default to skipping even if a trigger fires):**
- Debugging — work is bounded by the bug, few preferences surface
- Code review — reactive, framed by existing code
- Mechanical refactors, renames, dependency bumps
- Status / Q&A sessions, single-file edits
- Routine maintenance where the user mostly says "yes do it"

If the session is mixed (e.g. planning then implementation), reflect on the generative part only and ignore the rest.

## When to invoke

**Explicit triggers** — run immediately, no asking:
- "wrap up", "wrap this up", "journal this session"
- "reflect on this session", "save a reflection"
- "/journal" or any phrasing referring to the journal skill by name

**Implicit triggers** — *ask first*, with one short question, **only if the session was generative** (per the categories above):
- The user is about to run `/compact` or just ran it.
- The user signals the session is ending: "we're done", "let's call it", "good stopping point", "I'll come back tomorrow", "shutting down for the day".
- The user asks you to summarise the session in a way that smells like wrap-up rather than progress-tracking.

If the session was reactive (debugging, code review, mechanical edits) and the trigger is implicit, **stay silent** — don't even ask. The user can still invoke explicitly if they disagree.

If the answer to your offer is no, drop it. Do not ask twice in the same session.

## The skip rule

The session-kind filter above is the first gate. Within a generative session, there's a second gate: if **nothing was surprising, redirecting, or instructive** about how the user works, still skip. Empty calories hurt the signal. Concretely, skip if all of the following are true:

- The user made no choices between options you offered.
- You did not change direction based on feedback.
- The user did not approve a non-obvious approach.
- There were no friction points worth naming.

When in doubt within a generative session, ask: "I don't see anything notable enough for a reflection — agree?" Let the user override. For a reactive session that hits an implicit trigger, just stay silent — don't ask.

## The process-regression exception

The session-kind filter optimises for capturing *preferences*. A workflow breaking down is not a preference, so the filter makes the most important events invisible — a reactive session can still carry the highest-signal information available: evidence that the way the user works has stopped working.

Reflect regardless of session kind when any of these appear:

- Work had to be redone — a plan superseded, an implementation reverted or refactored soon after landing.
- The user changed their workflow (different tooling, different model split, a step they normally take was skipped), or comments on the workflow itself.
- The user expresses reduced confidence in the output, the codebase, or the process.
- A previously recorded **Change** lesson visibly recurred.

Keep these short and aimed at the *process*, not the technical fix. The entry is "the plan's premise was never validated and no step in the workflow would have caught it"; what the premise was is context.

## Drafting

Read the canonical template and folder layout from `~/.claude/journal/README.md` before drafting. That file is the source of truth — if it has diverged from this skill, follow it.

**First run:** if `~/.claude/journal/README.md` does not exist, the journal hasn't been set up yet. Create `~/.claude/journal/reflections/` and `~/.claude/journal/distilled/`, copy `assets/journal-README.md` to `~/.claude/journal/README.md`, and mention that you've done so. The user owns that file from then on — it is theirs to edit, and the skill follows it rather than overwriting it.

What goes in (focus rigorously on these):

- **How the user iterated** — the cadence. Did they open broad and narrow down? Add requirements mid-stream? Lock things via AskUserQuestion or via direct correction?
- **Reactions** — what they liked, what they pushed back on, and especially **what they silently accepted**. Silent confirmations are usually the highest-signal entries because the user doesn't volunteer them.
- **Keep / Change** — concrete behaviours for Claude to repeat or stop. Each entry should be specific enough that another Claude reading it months later could act on it.
- **Open threads** — unresolved tensions or follow-ups, including the work that came out of the session.

What stays out:

- A summary of *what was built*. (That's in the code / PR / plan file.)
- The technology choices themselves, unless the user reacted to them.
- Praise for either party. "Good session" is not a reflection.

If your draft starts to read like a project status update, you are off-track. Cut the technical content and re-focus on the *meta* layer — how the collaboration went.

## Length & tone

Match the tone of `assets/reflection-example.md` — or of the user's own recent reflections once a few exist, since those reflect how they actually write. That is: candid, specific, short sentences, bullets over prose, named patterns ("structured questions in batches of 3–4") over vague impressions ("communication was good"). Aim for ~250–500 words. Longer is OK only if there were genuinely multiple notable patterns.

## Ritual

1. **Decide** whether the session warrants a reflection (see skip rule). If unsure, ask once.
2. **Choose a filename** — `YYYY-MM-DD-<short-slug>.md` in `~/.claude/journal/reflections/`. Slug should be 2–4 words capturing the subject; lowercase, hyphen-separated. If a file already exists for today's date with this slug, append a `-2` (etc.) rather than overwriting.
3. **Draft** using the template. Lean on signals already in the conversation; don't fabricate reactions the user didn't have.
4. **Show the draft in chat first**, then ask for edits. Do not save before showing.
5. **Save** to the target path after the user confirms or edits. Use the Write tool.
6. **Check for a repeat.** Compare this reflection's **Change** entries against earlier reflections. If one restates a lesson already recorded, that is the promotion signal — say so and act on it this session (see **Promotion**). Do not queue it for a distillation cycle.
7. **Offer distillation** only when conditions are met (see below). Do not offer reflexively — it adds friction.

## Promotion — the delivery half

A reflection nobody reads changes nothing. Capture is half the loop; **promotion is what makes a lesson act on a future session**, because reflections are never loaded into context and skills and auto-memory always are.

When a **Change** entry repeats one from an earlier reflection, promote it the same session. Ranked by durability:

1. **Into a skill** — if the lesson belongs to a phase that already has one (planning → `plan-kickoff`, execution cadence → `shape-dd`), a rule there fires every time that skill triggers. Strongest form. If the skill carries a **Local calibration** section, person-specific values and preferences belong there rather than in the general rules — that separation is what keeps the skill shareable while still absorbing what you learn.
2. **Into auto-memory** as a `feedback` entry — for lessons that cut across phases.
3. **Left in the journal** — fine for anything not yet clearly recurring, but understand it will influence nothing until promoted.

Never promote without explicit confirmation. But always *raise* it: a third occurrence of the same Change entry is a defect in the loop, not another data point.

## Distillation (occasional, not every time)

After saving, list files in `~/.claude/journal/reflections/`. Offer to synthesise when **either** 5+ reflections are newer than the last modification time of `~/.claude/journal/distilled/preferences.md`, **or** 30 days have passed since it was last modified and at least one reflection is newer. (If `preferences.md` does not exist, 5+ reflections total.) A fixed count silently disables distillation whenever the journal goes quiet — which is exactly when the gap is worth examining.

> "There are N new reflections since the last distillation — want me to refresh `distilled/preferences.md`?"

If the user says yes:
- Read every reflection newer than the current `preferences.md`.
- Produce a concise (~30–60 short bullets), categorised summary: **Iteration patterns**, **What works**, **What to avoid**, **Open tensions**. No narrative; pure rules.
- Save to `~/.claude/journal/distilled/preferences.md`. Overwrite is fine — distilled files are derivative.

Promotion is handled per-reflection at Ritual step 6, not deferred to here — by the time five reflections have accumulated, a recurring lesson has already cost several sessions.

## Edge cases

- **The user runs the skill but the session is empty / brand-new** — there's nothing to reflect on. Say so and stop.
- **The conversation has been compacted** — work from what's in the current context; flag that earlier signal may have been lost.
- **The user asks for a reflection on a *previous* session** — you don't have that context. Offer to start a fresh reflection for what they remember instead, and write it from their words.
- **A long gap since the last reflection** — if the newest reflection is 30+ days old, say so and ask one question: what changed in between? A quiet journal usually means the work moved somewhere the triggers don't fire, and that answer is worth more than the current session's entry.
- **Multiple sessions in one day** — append `-2`, `-3`, etc., or merge into one file if the topics are continuous and the user prefers.
- **The user wants the reflection private / not promoted to memory** — fine. The journal is theirs; never auto-promote to auto-memory without confirmation.

## Why this matters

The goal is a portable read on how someone works — over time the distilled preferences should be paste-able into a fresh session (or surfaced by a session-start hook) so a new agent starts oriented instead of cold. Each reflection is a data point toward that. The reason to capture **reactions, not technical content** is that technical content rots quickly (codebases change), while how a person thinks about collaboration changes slowly. The slow-moving layer is what compounds.
