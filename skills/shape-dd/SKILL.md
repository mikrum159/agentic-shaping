---
name: shape-dd
description: Keep AI-assisted software work aligned through Shape-Driven Agentic Development (also called Agentic Sculpting) - rough Intent, a compact Current Shape, and one reviewable unit at a time (Build Slice, Decision Slice, Re-cut, or Pass), each agreed before building and captured after. Use when starting from rough intent, distilling an existing plan/spec/issue into a shape, resuming work without chat history, implementing, deciding an open question, re-cutting the slice list, reviewing, polishing, or improving feature/refactor/fix work that needs controlled iteration without a heavyweight spec. Avoid for pure Q&A, one-off edits that need no persistent context, or work that truly needs formal specifications, product discovery, project management, or architecture documentation.
---

# Shape-Driven Agentic Development

A lightweight anti-drift workflow between vibe coding and spec-driven development.

Loop: `Intent -> Current Shape -> Candidate Slices -> Selected unit -> Build -> Review -> Capture -> Next unit`

## Stance

The plan is meant to move. Start from rough Intent and a compact Shape, not a spec — over-specifying upfront is what drives over-build and false precision. As findings land, the plan and the result are **expected** to diverge from where they started. That is the method working.

So "anti-drift" does not mean stick to the plan. It means changing course is a deliberate, named, captured move — a Re-cut or a Decision Slice — instead of a silent slide. Nothing in the slice list is mandatory; each unit is re-evaluated when it comes up.

## Vocabulary

- **Intent** — what the work is trying to achieve and why. Rough, not a spec.
- **Current Shape** — the compact living state: understanding, decisions, constraints, assumptions, risks, open questions, next units.
- **Slice** — one reviewable unit. The implementation, review, and capture boundary. *Not* necessarily the conversation boundary — see Checkpoint.
  - **Build Slice** — the default. A code or artifact change.
  - **Decision Slice** — resolves an open question that would otherwise change future Build Slices. Output is updates to Decisions / Constraints / Open questions, optionally a spec doc. No code required; resolving the question *is* the unit.
- **Re-cut** — revises the Candidate Slice list (split, merge, reorder, insert, drop). Sits between units, never inside one. Gets its own capture.
- **Pass** — smaller than a Slice: polish, cleanup, narrow correction, planning. No row in the slice list; still gets its own capture.
- **Checkpoint** — a pause *inside* a unit. Three or four lines, no agreement ritual, no capture, no new unit. **Silence is proceed.**
- **Shape Pass** — one iteration of the loop. Ends with a capture.

Naming all four unit kinds is what stops every step being forced into a "write code" frame, and stops the slice list changing silently.

## The loop

### 1. Before the unit — agree

Give a short plain-language orientation the developer can judge *without opening the shape file*:

- **goal** — what this step does
- **scale** — rough size
- **boundary** — what it touches, and what it deliberately leaves alone
- **architecture** — anything it commits to
- **still right?** — whether this is still the right next unit, and anything in the slice list that should change
- **kind** — Build Slice / Decision Slice / Re-cut / Pass, tagged at the end, not as the headline

Then invite challenge and **wait for explicit agreement** before editing code, artifacts, or the shape file. If the orientation surfaces tension with the developer's vision, architecture, or approach, pause for discussion or a Decision Slice before touching code.

A kind label names the workflow state, not whether the move is *right*. Goal, scale, boundary and architecture are what let the developer judge the move itself.

Slice entries are rough direction and validation targets, not prescriptive plans — the exact scope is agreed here, in conversation, just before building. Without that, the slice list gets read as a fully-specified plan and the unit over-builds. For a Decision Slice, "the change" is updates to the Current Shape plus optional docs; same agreement step, naming the question and the options weighed.

Once a shape has several units behind it, the **still right?** check extends to the model itself: is it still right, what has been added that could now be deleted, and which Decision or Constraint is doing the most load-bearing work — is it still true, and if it came from a document, is that document still true? Answer in one line. If the answer is not "no change", propose a Re-cut. This is the only step that can *shrink* the design rather than extend it.

Ask a question, rather than assuming, when:

- multiple choices would lead to meaningfully different code
- the next step depends on a product, data, API, security, UX, or architecture decision
- the boundary or validation is unclear enough that review would be unreliable
- the request conflicts with the Current Shape

Otherwise state the assumption briefly and proceed.

### 2. During the unit — stay in scope

- Make only the changes the unit needs. No opportunistic refactors outside the boundary.
- If the unit proves too large, narrow it inline and split the remainder off as a later candidate. That is the only slice-list edit allowed inside an in-flight unit; anything broader is a Re-cut.
- **Checkpoint** at natural seams: what landed, what's next inside this boundary, anything found that might change the plan. Then continue unless redirected.

Checkpoint when a layer or file group completes, when a finding arrives that doesn't warrant a Re-cut, or when the unit is running long enough that one end-of-unit capture would lose the early detail. On a multi-session unit, append each checkpoint to the log as you go.

Correction opportunity and unit size are different knobs. Fusing them is what drives slices to shrink until every one carries a full agree → build → show → capture ceremony. Keep units the size `references/sizing.md` describes and pause *within* one instead of cutting another.

### 3. After the unit — review, show, don't commit

Check, before showing:

1. actual changes against the goal and boundary
2. validation results, or missing validation. Before iterating on a *failing* validation, confirm the instrument observes what it should — a failing test, empty query, or missing log line can mean broken code **or** a broken oracle. Iterating with a broken instrument wastes rounds and hides the real signal.
3. decisions, tradeoffs and surprises worth capturing
4. follow-up work, named without expanding this unit
5. external standards — a checklist, the project's `CLAUDE.md`, a bootstrap recipe. A unit can be complete by its own goal and still fail one; without the audit the gap stays merged.

Then surface the diff and validation results, and **stop**. Never commit or push (see *Local calibration*). Do not chain consecutive units in one pass — even tightly-related follow-on work is its own pass with its own agreement. Steps inside one unit's agreed boundary are Checkpoints and need no re-agreement.

### 4. Capture

Required for every unit kind. The capture is what makes work resumable across sessions; the interview steps are optional, this is not.

Read `references/capture-formats.md` when writing one — it carries the per-kind fields and the end-of-pass checklist.

Capture when the unit ends, and also whenever the developer asks any version of *"anything to update before I commit?"* — that question means close the pass, not just append notes.

A unit is not captured until validation has landed. Built-but-unvalidated work goes under **Pending validation**, never under Completed units.

## Sizing

If you can state a unit's boundary in one sentence and validate it against a single goal, the size is probably right. Multiple unrelated validations, or a boundary that's hard to state, usually means two units — but check first whether you actually want a Checkpoint.

Read `references/sizing.md` when a boundary feels off.

## Starting a new shape

1. Restate the Intent in one or two sentences.
2. Create the Current Shape from `assets/shape-template.md`.
3. Identify known constraints and unknowns.
4. Propose 2-4 Candidate Slices.
5. Recommend one Selected unit. If a Decision Slice is the honest next step, say so — do not invent a Build Slice that papers over an unresolved choice.
6. Stop before implementation unless asked to build immediately.

Keep the opening short: one or two Intent sentences, a few Shape bullets, 2-4 Candidate Slices, one recommended unit, a pause. `examples/opening-response.md` is the density target. Don't ask for more detail unless a missing decision blocks the next unit.

**From an existing plan, spec, issue or design note:** treat it as source material, not a work order. Do not execute it directly. Distill it into the shape first — intent, constraints, known decisions, assumptions, risks, open questions, candidate slices, recommended next unit (often a Decision Slice, if the plan has unresolved choices). A detailed plan can inform the shape; it does not replace it.

Record where each constraint and decision came from. Anything inherited from a document — including a plan that itself leaned on a note somewhere in the repo — is a claim with a source, not a verified fact, and a stale one reads exactly like a real limit. A long plan can't be audited up front, so provenance is what makes the check possible later, at the moment one actually blocks a unit.

## Resuming existing work

1. Read the Current Shape first, then the log's most recent entries.
2. Honor the shape's Working Agreement.
3. Reconcile state before proposing anything: if the tree is clean and the work is committed but a unit is still open, or an entry sits under Pending validation whose validation has already passed, close it out as the first action rather than asking the developer to adjudicate.
4. Summarize the current state briefly.
5. Propose the next unit, or continue the selected one.
6. Preserve captured decisions and constraints unless new evidence changes them. Ignore stale chat context that conflicts with the Current Shape.

## Artifacts

- Small task: `docs/shapes/{task-name}-shape.md` — state and log in one file.
- Larger or multi-session task: `docs/shapes/{feature}-shape/shape.md` (state) + `log.md` (append-only history), optionally `slices/001-{name}.md`.

Use the single file until the work clearly needs more.

**Locating shapes:** don't assume `docs/shapes/` exists. Look for `**/shapes/**/*shape*.md` or `**/*-shape.md` first. If none exists and the repo has no `docs/`, ask before creating one; if the repo already has a home for design notes (`docs/`, `notes/`, `.agents/`), put shapes alongside it.

**Templates:** `assets/shape-template.md` (state), `assets/log-template.md` (history), `assets/slice-template.md` (separate slice records), `assets/skill-feedback-template.md` (process friction).

**Closing:** a shape doesn't have to deliver every Candidate Slice to be worth closing. Close at a coherent stopping point — when what shipped forms a self-contained chapter — flip Status to `Closed` with a short closure summary (what shipped, what was deferred, where it went), and move remaining items to a successor shape that links back. Prune Decisions at close: mark superseded entries `[superseded by …]` or move them to an archive section. Inside an active shape, strike through rather than delete — the original wording is often useful evidence for the successor.

Split instead of closing when two themes inside one shape stop sharing context. Fork instead of splitting when an idea is only loosely related — new shape, cross-linked.

**Archiving:** shape files usually aren't committed, so a closed shape dies with its branch — taking the log and the Skill Feedback with it. When the developer asks to archive (typically before opening the PR), follow `references/archiving.md`.

## Delegating to sub-agents

Delegate a unit when it is self-contained enough for a one-shot brief *and* mechanical enough that briefing costs less than doing. Keep it direct when it is one line, judgment-heavy, or depends on context already loaded. Captures and Decision Slices always stay in-context.

Read `references/delegation.md` before writing a brief.

## Local calibration

Defaults tuned to one developer. Edit freely — lessons about how *this* developer works land here rather than rewriting the rules above.

- **Never commit or push.** Show the diff and stop; the developer commits. Only an explicitly autonomous session, agreed in the shape's Working Agreement, changes this.
- **Prefer one larger unit with Checkpoints over two small ones.** If a unit's capture would be a single line, it is a Pass, or it belongs merged with its neighbour.
- **Expect roughly one unit per session.** Keep `Resume next session` accurate enough that a cold session can act from it without reading the whole shape.
- **Delegate mechanical work to a cheaper model tier**; keep orchestration, captures and Decision Slices in-context.
- **Archive closed shapes** to `~/.claude/shape-archive/{repo}/{date}-{feature}/`.
- **Don't solicit process moves.** Propose a Re-cut, a model re-check, or an extra validation round only when a trigger in the loop actually fired — not as a standing offer.

## Skill improvement

This skill is usage-informed but not self-mutating.

During product work, capture friction only as Skill Feedback (`assets/skill-feedback-template.md`): repeated confusion, missing template fields, unclear boundaries, too much ceremony, terminology that caused mistakes, or patterns the developer invented mid-flow because the skill didn't acknowledge them. That last one is the strongest signal — a section added to a shape file by hand probably belongs in the template.

Review feedback after the product shape is implemented or paused. Change this skill, its templates, or its examples only during an explicit skill-improvement Shape Pass. Suggest at most one or two focused improvements at a time.

## Output style

Compact and operational. A short Shape update, a short list of Candidate Slices, one recommended unit with its kind, direct capture notes after review. Be critical of over-planning, context bloat, vague abstractions, and drift. Skip methodology explanations unless asked.
