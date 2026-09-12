---
name: shape-dd
description: Guides AI-assisted software development through Shape-Driven Agentic Development, also called Agentic Sculpting - rough Intent, compact Current Shape, one reviewable unit (Build Slice, Decision Slice, Re-cut, or Pass), review, and capture. Use when starting from rough intent, distilling an existing plan/spec/issue into a shape, resuming, implementing, deciding an open question, re-cutting the slice list, reviewing, polishing, or improving feature/refactor/fix work that needs controlled iteration without a heavyweight spec. Avoid for pure Q&A, one-off edits that need no persistent context, or work that truly needs formal specifications, product discovery, project management, or architecture documentation.
---

# Shape-Driven Agentic Development

Use this skill to keep AI-assisted software work aligned through a compact Current Shape and small reviewable units.

## Core idea

Shape-Driven Agentic Development, also called Agentic Sculpting, is a lightweight anti-drift workflow for software work with AI agents.

It sits between casual vibe coding and heavier spec-driven development.

Default loop:

`Intent -> Current Shape -> Candidate Slices -> Selected Unit -> Build/Revise -> Review -> Capture -> Next Unit`

A Shape Pass is not complete until the Current Shape is updated.

### Stance (read this first)

The plan is meant to move. You start with a rough Intent and a compact Shape — not a full spec — because over-specifying upfront is what drives over-build and false precision. As real findings land (a constraint, a concrete example, an architecture decision made in conversation), the plan and the final result are **expected** to diverge from where they started. That is the method working, not failing.

So "anti-drift" does **not** mean "stick to the plan." It means changing course is a *deliberate, named, captured* move — a Re-cut or a Decision Slice — instead of a silent slide. Flow with the Shape; change direction when findings or developer discussion warrant it; just keep each change small, explicit, and written down so the work stays reviewable and resumable.

Think of it as sculpting: a rough form first, refined as the material reveals itself — not a blueprint executed to spec.

## Vocabulary

- **Intent**: the guiding artifact. States what the work is trying to achieve and why, without becoming a large upfront spec.
- **Current Shape**: the compact, living state of the work — current understanding, decisions, constraints, assumptions, risks, open questions, completed work, and likely next units.
- **Slice**: a small, reviewable unit of work. It is the implementation boundary, the review boundary, and the capture boundary. It is *not* necessarily the conversation boundary — see **Checkpoint**. Slices come in two flavors:
  - **Build Slice**: the default — a small reviewable code or artifact change.
  - **Decision Slice**: resolves an open question whose answer would change future Build Slices. Output is updates to Decisions / Constraints / Open questions in the Current Shape, possibly with an idea/spec doc. No code required, and that is fine — resolving the question IS the reviewable unit.
- **Re-cut**: revises the Candidate Slice list itself (split, merge, reorder, insert, drop) in response to new information. Sits between Slices, never inside one. Has its own Capture entry stating what changed and why.
- **Pass**: a unit smaller than a Slice — polish, chrome, cleanup, narrow correction, planning. Doesn't deserve its own row in the slice list, but does deserve its own Capture entry rather than being bundled into the next Slice's notes.
- **Checkpoint**: a pause *inside* a Slice. A short summary of what landed and what's next, with an open invite to redirect — no agreement ritual, no capture entry, no new Slice. Checkpoints are how a Slice stays PR-sized without the developer losing the chance to change course mid-unit.
- **Shape Pass**: one iteration through the loop. A Shape Pass can be a Build Slice, a Decision Slice, a Re-cut, or a Pass. Each ends with a Capture.

The vocabulary exists because all four kinds of unit happen routinely in real work. Naming them keeps the agent from forcing every pass into a "build code" frame and prevents the slice list from drifting silently.

## When to use

Use this skill when the user wants to:

- start a new AI-assisted software feature, refactor, fix, migration, or investigation
- use an existing plan, spec, issue, design note, or implementation outline as starting context
- resume work without relying on full chat history
- break rough intent into small reviewable changes
- resolve an open question (Decision Slice) without inventing code
- re-cut the slice list when new information lands
- record a polish/cleanup/planning pass that's smaller than a Slice
- constrain an agent before implementation
- review a completed unit and update persistent context
- improve this skill after observing real workflow friction

## When not to use

Do not expand this into a heavyweight process.

Avoid this skill for:

- pure explanations or Q&A
- trivial edits that do not need persistent context
- work that needs formal requirements, product discovery, project management, or architecture documentation
- broad multi-feature planning unless the user explicitly asks for it

If a heavier spec-driven process is more appropriate, say so briefly and keep the suggestion narrow.

## Operating rules

1. Work one unit at a time (one Slice, one Decision, one Re-cut, or one Pass).
2. Slice entries in the Current Shape are **rough direction and validation targets**, not prescriptive implementation plans. The exact scope of each unit is agreed in conversation just before building. This is the most common source of drift — without an explicit per-pass agreement, the slice list often gets read as a fully-specified plan and the agent over-builds.
3. Resolve blocking unknowns with a **Decision Slice** rather than guessing inside a Build Slice. A Decision Slice that produces no code is allowed and expected when the next Build Slice depends on a question that has not been resolved.
4. When new information would re-shape the slice list (split, insert, reorder, drop), propose a **Re-cut** as the next pass. Do not silently edit the slice list while another unit is in flight.
5. Maintain the Current Shape instead of relying on chat history.
6. Keep files short, practical, and reusable.
7. Be critical of over-planning, context bloat, vague abstractions, and agent drift.
8. Suggest at most one or two focused process improvements at a time.
9. Do not silently change this skill, its terminology, or its core process during product work. Capture friction as Skill Feedback and apply it during a dedicated skill-improvement Shape Pass.

### Sizing each kind of unit

Quick rule: if you can state the unit's boundary in one sentence and validate it against a single goal, the size is probably right. Multiple unrelated validations or a hard-to-state boundary usually means two units.

For detail on Build Slice / Decision Slice / Re-cut / Pass sizing, read `references/sizing.md` when a boundary feels off.

## Developer-agent collaboration

Treat the developer-agent interaction as a tight shaping loop, not a one-way command.

Before any unit of work starts, give a short plain-language orientation the developer can judge *without opening the shape file*: what the step does, its rough scale, the boundary (what it touches and what it deliberately leaves alone), and any architecture it commits to — with the unit kind (Build Slice / Decision Slice / Re-cut / Pass) tagged at the end, not as the headline. Then invite challenge: if any of it conflicts with the developer's vision, architecture, or preferred approach, pause for discussion or a Decision Slice before touching code. Wait for explicit agreement.

A label like "Re-cut" or "Decision Slice" names the workflow state but not whether the move is *right*; leading with goal, scale, boundary, and architectural stakes lets the developer judge the move itself. The cost of one extra round trip is small; the cost of an over-stuffed slice that has to be rolled back is much larger. (See operating rule #2 for why the slice list alone is not enough.)

The agent should:

- preserve the developer's stated intent
- clarify only decisions that materially affect the current pass
- state reasonable assumptions instead of blocking on minor unknowns
- point out risks, inconsistencies, missing validation, and likely technical debt
- suggest narrower or safer units when requested work is too broad, vague, or risky
- recommend a Decision Slice or Re-cut when those are the more honest next step instead of forcing a Build Slice
- pressure-test the planned next unit against a concrete example before committing to it; if a real case (a specific workload, input, or edge case it can't honestly handle) exposes a hole, prefer a Re-cut over pushing through the planned order
- avoid expanding scope without explicit user agreement

Ask questions when:

- multiple choices would lead to meaningfully different code
- the next step depends on a product, data, API, security, UX, or architecture decision
- the boundary or validation is unclear enough that review would be unreliable
- the request conflicts with the Current Shape

Otherwise, proceed with stated assumptions and capture open questions in the Current Shape.

## Using existing plans

If the user provides an existing plan, spec, issue, design note, implementation outline, or similar source, treat it as source material.

Do not execute the full plan directly.

First distill it into the Current Shape:

- intent
- relevant constraints
- known decisions
- assumptions
- risks
- open questions
- candidate slices
- recommended next unit (often a Decision Slice if the plan has unresolved choices)

A detailed plan can inform the shape, but it does not replace the shape.

## Artifact choices

Default paths:

- Small task: `docs/shapes/{task-name}-shape.md`
- Larger task: `docs/shapes/{feature-or-task}-shape/shape.md`
- Optional Slice files for larger work: `docs/shapes/{feature-or-task}-shape/slices/001-{slice-name}.md`

Use the single-file shape unless the work clearly needs multiple passes or separate Slice records.

### Locating shapes

When resuming or creating, do not assume `docs/shapes/` exists. First look for an existing shape with a glob like `**/shapes/**/*shape*.md` or `**/*-shape.md`. If none exists and the repo has no `docs/` directory, ask before creating one rather than introducing a new top-level folder. If the repo already has a conventional location for design notes (`docs/`, `notes/`, `.agents/`, etc.), prefer placing shapes alongside it.

When creating a new shape, use `assets/shape-template.md`. The template ships with a **Working Agreement** section that captures agree-before-build / show-before-commit defaults; keep it, edit it, or replace it, but don't silently delete it.

When creating a separate Slice file, use `assets/slice-template.md`.

When capturing process feedback for the skill itself, use `assets/skill-feedback-template.md`.

Use examples only when the user needs a concrete model:
- `examples/single-file-shape.md`
- `examples/feature-folder-shape.md`
- `examples/opening-response.md`

### Closing a shape vs. spawning a successor

A shape doesn't have to deliver every Candidate Slice to be worth closing. Close at a coherent stopping point — when what's shipped forms a self-contained chapter — and move remaining items to a successor shape. The successor links back; the closed shape's Status flips to `Closed` with a short closure summary listing what shipped, what was deferred, and where it went. This keeps individual shapes small enough to read in one sitting and prevents Decisions/Risks from accumulating past their useful life.

Split rather than close-and-spawn when two themes inside one shape stop sharing context (e.g. infra setup vs. UI polish on the same feature). Fork rather than split when an idea surfaces that's only loosely related — start its own shape from scratch and cross-link.

## Starting a new shape

When the user provides rough Intent:

1. Restate the Intent in one or two sentences.
2. Create or update the Current Shape (including the Working Agreement section from the template).
3. Identify known constraints and unknowns.
4. Propose 2-4 Candidate Slices.
5. Recommend one Selected unit. If a Decision Slice is the honest next step, say so — do not invent a Build Slice that papers over an unresolved choice.
6. Stop before implementation unless the user asked to build immediately.

Do not ask for more detail unless a missing decision blocks the next unit. If reasonable assumptions are enough, state them briefly and proceed.

### Example response shape

Opening responses are short — one or two Intent sentences, a few Current Shape bullets, 2-4 Candidate Slices, one recommended Selected unit, and a pause. See `examples/opening-response.md` for a concrete model.

## Resuming existing work

When a Current Shape or shape file already exists:

1. Read the Current Shape first.
2. Honor any Working Agreement defined in the shape.
3. Ignore stale chat context if it conflicts with the Current Shape.
4. Summarize the current state briefly.
5. Propose the next unit (Build Slice, Decision Slice, Re-cut, or Pass) or continue the selected one.
6. Preserve decisions and constraints already captured unless new evidence changes them.

## Compressed loop

Real users sometimes skip straight to "just build it" mid-flow. That is fine — the interview steps are optional, the Capture is not.

When the loop is compressed:

- Keep each unit Slice-shaped (one reviewable change, narrow boundary).
- Pause after each unit and surface the diff before committing. Do not chain consecutive units in a single pass even when both feel small. Two small Passes is two captures and two review points; a chained pair is one untestable unit. (Steps *inside* one Slice's agreed boundary are Checkpoints, not chained units.)
- Write a short Capture inline when the pass ends.

The Capture step is what makes work resumable. The interview steps are optional; the Capture is not.

## Building or revising a unit

The three phases below are the heart of the anti-drift loop. The Capture step at the end depends on having a clear boundary that was agreed up front and validation that was reviewed before commit.

### Before building (agree)

1. Give the short orientation from *Developer-agent collaboration* — what the step does, its scale, its boundary, and the architecture it commits to — with the unit kind (Build Slice / Decision Slice / Re-cut / Pass) tagged at the end.
2. State the goal and explicit boundary in one short paragraph the developer can challenge, and invite challenge to the approach before any code is touched.
3. List expected validation.
4. Wait for explicit agreement before editing code, artifacts, or the shape file beyond the proposal itself.

For a Decision Slice, "the change" is updates to the Current Shape itself plus optional spec/idea docs — not code. The same agreement step applies: name the question being resolved and the options being weighed.

### While building (stay in scope)

- Make only changes needed for that unit.
- Avoid opportunistic refactors unless they are inside the boundary.
- If the implementation reveals the unit is too large, narrow it inline (split off the remainder as a later candidate). That is the only kind of slice-list edit that belongs inside an in-flight unit. Anything broader — re-ordering, inserting new units, reshaping multiple downstream entries — is a Re-cut and gets its own pass.

### Checkpoints inside a unit

Correction opportunity and unit size are different knobs, and fusing them is what drives slices to shrink: if the only way to get another look is to cut another Slice, slices get cut smaller and smaller until every one carries a full agree → build → show → capture ceremony and the loop reads as overhead.

So keep Slices at the size `references/sizing.md` describes — one concern, one validation criterion, roughly PR-sized — and pause *within* one at a natural seam. A Checkpoint is three or four lines:

- what landed since the last checkpoint,
- what's next inside this Slice's boundary,
- anything found that might change the plan.

Then continue unless redirected. **Silence is proceed** — no approval needed. That asymmetry is what keeps it cheap: an agreement gate costs a round trip every time, a checkpoint costs one only when it's used.

Checkpoint when a layer or file group completes mid-Slice, when a finding arrives that doesn't warrant a Re-cut but the developer would want to know, or when the Slice is running long enough that one end-of-slice capture would lose the early detail. On a multi-session Slice, append each checkpoint to the running log — that is the interim progress the capture section asks for.

A Checkpoint is not a Pass. A Pass is its own unit with its own capture; a Checkpoint is punctuation inside one.

### After building (show, don't commit)

- Surface the diff and validation results to the developer.
- Wait for explicit approval before committing, pushing, or moving to the next unit.
- Do not chain consecutive **units** in a single pass. Even tightly related follow-on work (1b after 1a, polish after a Slice, deploy after a build) is its own pass with its own agreement and review. This is about units — steps inside one Slice's agreed boundary are Checkpoints, and need no re-agreement.

### Delegating to sub-agents

Some passes are mechanical enough that handing them to a smaller sub-agent costs less than doing them directly; others are not, and the briefing overhead exceeds the savings. The orchestrator's job is to spot which is which.

Delegate when both hold:
- the unit is self-contained enough that a one-shot brief can describe it fully (no live conversational context needed),
- it is mechanical or well-bounded enough that briefing cost is less than doing cost.

Keep direct when the unit is one line, judgment-heavy, or depends on context the agent already has loaded. Captures and Decision Slices stay in-context — they depend on full conversation state and judgment, and are not delegable.

Match the model tier to the judgment the work requires. On Claude Code that tends to look like an Opus main agent orchestrating, Sonnet sub-agents for bounded code edits plus build verification, and Haiku sub-agents for mechanical doc/text sweeps and research — but use whatever capable/cheaper split your agent supports; the tiering matters more than the names. Rule of thumb from practice: a single-line change is faster done directly (briefing overhead outweighs the saving), while a 3-file rename or a 15-edit doc sweep is worth the brief.

A brief that produces clean handoffs has four parts:
1. **Background**: what shape, what slice, why this change.
2. **In-scope changes**: exact files and exact edits.
3. **Out of boundary — do not touch**: the highest-value section; an explicit list prevents scope creep.
4. **Verification + report-back**: build/grep/test step and the format you want results in.

Trust but verify: read the diff and re-run validation yourself before accepting. Briefs should explicitly cover ambiguous edge cases — sub-agents have no chat context and will interpret narrowly.

## Reviewing a unit

When reviewing a completed unit:

1. Compare actual changes against the goal and boundary.
2. Check validation results or identify missing validation. Before iterating on a *failing* validation, first verify the validation instrument observes what it should — a failing test, empty query, or missing log line can mean broken code OR a broken oracle. Confirm the oracle first; iterating on a fix with a broken instrument wastes rounds and obscures the real signal.
3. Note decisions, tradeoffs, or surprises.
4. Identify follow-up work without expanding the current unit.
5. If external standards exist (a checklist, the project's `CLAUDE.md`, a bootstrap recipe), audit the unit against them before declaring it complete. A unit can be nominally complete by its own goal but fail an external standard; without the audit, the gap stays merged.

### Model review — the step-back pass

A Re-cut is reactive: it fires when new information lands. Nothing else in the loop looks back at the *model itself* on a cadence, and small-unit work has a blind spot exactly there — building slice by slice, you never step far enough back to notice that three consumers each rebuild the same rule, or that the design fixed a symptom and left the shape.

So every third or fourth unit, spend one short pass on the accumulated shape rather than the next slice:

- Is the model still right, or has the work revealed a better one?
- What has been added that could now be deleted?
- Which Decision is doing the most load-bearing work, and is it still true?

Output is either "no change" — one line in the capture — or a Re-cut. It is a Pass, and it is cheap. It is also the only step in the loop that can *shrink* the design rather than extend it.

## Capturing after a Shape Pass

At the end of each Shape Pass, update the Current Shape. The capture step is required regardless of unit kind — it is what makes work resumable across sessions and reduces agent drift over time.

A unit is not fully captured until validation has landed. If a Build Slice was built but not yet validated, keep it under a **Pending validation** subsection of the shape, not under Completed units. Move it down once validation has passed and the entry is final. This split prevents a future session from reading "Completed" entries as verified when some are merely built.

Per-kind capture formats (Build Slice / Decision Slice / Re-cut / Pass) live in `references/capture-formats.md`. Read it when writing the capture so the right fields land.

For a long or multi-session Slice, append interim progress to the running log as you go rather than relying on one capture at the very end — a single consolidated capture works for a same-day Slice, but on a multi-day one the early detail is usually lost by the time it ends.

### Pruning Decisions at close

The Decisions block grows monotonically by default and accumulates superseded entries. When closing a shape, prune: mark superseded entries `[superseded by …]` or move them to an archive section so the load-bearing decisions are easy to find. Inside an active shape, prefer striking through rather than deleting — the original wording is often useful evidence for the successor.

## Skill improvement

shape-dd is usage-informed but not self-mutating.

During product work, capture skill/process friction only as Skill Feedback (use `assets/skill-feedback-template.md`). Examples of what is worth capturing:

- repeated confusion
- missing template fields
- unclear boundaries
- too much ceremony
- terminology that caused mistakes
- prompts that agents repeatedly misunderstood
- patterns the user invented mid-flow because the skill didn't acknowledge them (often the strongest signal — if a user adds a section to their shape file by hand, that section probably belongs in the template)

Usually review Skill Feedback after the product shape is implemented or paused.

Only change this skill, templates, or examples during an explicit skill-improvement Shape Pass.

### Measuring whether the loop earns its keep (optional)

The skill's central bet is that agree-before-build prevents over-build and drift. That bet is checkable. A few numbers, tallied in the capture (and surfaced by any session-reflection habit), turn it from a feeling into evidence across shapes:

- **redirects** — times the pre-step summary got the planned unit *changed before building* (the challenge step doing real work),
- **inline narrowings / rollbacks** — times a unit had to be shrunk mid-flight or undone (over-build slipping through anyway),
- **delegations + trust-but-verify catches** — units handed to sub-agents, and how often the diff review caught a real issue.

Keep it to a few numbers, not a scorecard. The strongest improvement signals come from *convergence* — the same friction showing up in the shape's Skill Feedback, a reflection, and a hand-edited section at once. If tracking these ever reads as ceremony, drop it; the point is signal, not bookkeeping.

## Output style

Keep responses compact and operational.

Prefer:

- a short Current Shape update
- a short list of Candidate Slices
- one recommended Selected unit (with kind: Build Slice / Decision Slice / Re-cut / Pass)
- direct capture notes after review

Avoid long methodology explanations unless the user asks.
