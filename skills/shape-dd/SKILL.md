---
name: shape-dd
description: Keep AI-assisted software work aligned through Shape-Driven Agentic Development (also called Agentic Sculpting) - rough Intent, a compact Current Shape, and one reviewable unit at a time (Build Slice, Decision Slice, Re-cut, or Pass), each agreed before building and captured after. Use only when the user explicitly asks for shape-dd or a shape (start a shape, distill a plan into a shape, propose or agree the next slice, close or archive a shape, a skill-improvement pass), or when resuming work from an existing shape file (one carrying the shape-dd Workflow header line, or under a shapes/ folder). Do not use for feature, refactor or fix work the user has not framed as shape work, pure Q&A, one-off edits, or work that needs formal specifications, product discovery, project management, or architecture documentation.
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
- **Review round** — the developer's feedback on a unit that has been shown but not yet accepted. It belongs to that unit: fix it, show it again, and note it in the unit's log entry. It needs no new agreement and does not become a new Pass.
- **Acceptance** — the developer's message closing the review, typically sent after staging (see *Local calibration*). It confirms the validation the developer owns and closes the unit in the same reply.
- **Shape Pass** — one iteration of the loop. Ends with a capture.

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

Checkpoint when a layer or file group completes, when a finding arrives that doesn't warrant a Re-cut, or when the unit is running long enough that one end-of-unit capture would lose the early detail. On a multi-session unit, append each checkpoint to the log as you go. Pause *within* a unit rather than cutting another one: see `references/sizing.md`.

### 3. After the unit — review, show, don't commit

Check, before showing:

1. actual changes against the goal and boundary
2. validation results, or missing validation. Before iterating on a *failing* validation, confirm the instrument observes what it should — a failing test, empty query, or missing log line can mean broken code **or** a broken oracle. Iterating with a broken instrument wastes rounds and hides the real signal.
3. decisions, tradeoffs and surprises worth capturing
4. follow-up work, named without expanding this unit
5. external standards — a checklist, the project's `CLAUDE.md`, a bootstrap recipe. A unit can be complete by its own goal and still fail one; without the audit the gap stays merged.

Then surface the diff and validation results, and **stop**. Never commit or push (see *Local calibration*). Do not chain consecutive units in one pass — even tightly-related follow-on work is its own pass with its own agreement. Steps inside one unit's agreed boundary are Checkpoints and need no re-agreement.

Until the developer accepts, any feedback on the unit is a **review round** inside it, not a new unit. Fix it, show it again, and stop again.

### 4. Capture

Required for every unit kind. The capture is what makes work resumable across sessions; the interview steps are optional, this is not.

Read `references/capture-formats.md` when writing one — it carries the per-kind fields and the end-of-pass checklist.

Capture in two moments. **When the unit is shown**, write its log entry with a status line, and list it under Pending validation if a check is still open. **On acceptance**, close the unit in that same reply: don't ask again, and don't leave it for the next session.

If the unit contained an argued-out divergence (a recommendation the developer overrode after discussion, or confusion about intent), offer the journal once in the closing message and name the moment. Otherwise don't mention it.

## Sizing

A unit is the right size if its boundary fits one sentence and it validates against a single goal. Read `references/sizing.md` when a boundary feels off.

## Starting a new shape

1. Restate the Intent in one or two sentences.
2. Create the Current Shape from `assets/shape-template.md`.
3. Identify known constraints and unknowns.
4. Propose 2-4 Candidate Slices.
5. Recommend one Selected unit. If a Decision Slice is the honest next step, say so — do not invent a Build Slice that papers over an unresolved choice.
6. Stop before implementation unless asked to build immediately.

Keep the opening short: one or two Intent sentences, a few Shape bullets, 2-4 Candidate Slices, one recommended unit, a pause. `examples/opening-response.md` is the density target. Don't ask for more detail unless a missing decision blocks the next unit.

**From an existing plan, spec, issue or design note:** treat it as source material, not a work order. Distill it into the shape before executing anything. When the plan has unresolved choices, the recommended next unit is often a Decision Slice.

Record where each constraint and decision came from. One inherited from a document is a claim, not a verified fact, and the recorded source is what lets it be checked when it blocks a unit.

## Resuming existing work

1. Read the Current Shape first, then the log's most recent entries.
2. Honor the shape's Working Agreement.
3. Reconcile state before proposing anything:
   - Read commit status from git, never from the shape.
   - Close validation you own yourself, such as a gate you can re-run.
   - **Never close a developer-owned check by inference.** A commit is not proof that the check ran. Ask one line ("Slice 17's restart check — did it pass?") and keep the check in Pending validation until the developer answers. If they skip the question, mark it `unconfirmed`.
4. Summarize the current state briefly.
5. Propose the next unit, or continue the selected one.
6. Preserve captured decisions and constraints unless new evidence changes them. Ignore stale chat context that conflicts with the Current Shape.

## Artifacts

- Small task: `docs/shapes/{task-name}-shape.md` — state and log in one file.
- Larger or multi-session task: `docs/shapes/{feature}-shape/shape.md` (state) + `log.md` (append-only history), optionally `slices/001-{name}.md`.

Use the single file until the work clearly needs more.

**Locating shapes:** don't assume `docs/shapes/` exists. Look for `**/shapes/**/*shape*.md` or `**/*-shape.md` first. If none exists and the repo has no `docs/`, ask before creating one; if the repo already has a home for design notes (`docs/`, `notes/`, `.agents/`), put shapes alongside it.

**Templates:** `assets/shape-template.md` (state), `assets/log-template.md` (history), `assets/slice-template.md` (separate slice records), `assets/skill-feedback-template.md` (process friction).

**Closing:** close when what shipped forms a self-contained chapter, even with Candidate Slices left; remaining items move to a successor shape that links back.
- **Audit first.** Run one review across everything the shape touched, rather than unit by unit. Re-check the guarantees earlier units claimed against the code, and anything left `unconfirmed`. Per-unit checks do not add up to a verified whole.
- **Fill the closure summary** in the log template, including `Audit:`, then flip Status to `Closed`.
- **Prune Decisions:** mark superseded entries `[superseded by …]`. Inside an active shape, strike through rather than delete.

Split instead of closing when two themes inside one shape stop sharing context. Fork instead of splitting when an idea is only loosely related — new shape, cross-linked.

**Archiving:** an uncommitted shape dies with its branch, taking the log and the Skill Feedback with it. A committed one still belongs in the archive, which gathers the record across repos. When the developer asks to archive (typically before opening the PR), follow `references/archiving.md`.

## Delegating to sub-agents

Delegate a unit when it is self-contained enough for a one-shot brief *and* mechanical enough that briefing costs less than doing. Keep it direct when it is one line, judgment-heavy, or depends on context already loaded. Captures and Decision Slices always stay in-context.

Read `references/delegation.md` before writing a brief.

## Local calibration

Defaults tuned to one developer. Edit freely — lessons about how *this* developer works land here rather than rewriting the rules above.

- **Never commit or push.** Show the diff and stop; the developer commits. Only an explicitly autonomous session, agreed in the shape's Working Agreement, changes this.
- **Acceptance** is any message that says the work is validated or staged and asks about committing or recording. Examples: "validated, staged. anything to record?", "staged, all ok. I'll commit - anything to record before I do?", "validated, staged. can I commit?". Any such message closes the unit in that reply. A message that asks for a change is a review round.
- **Compact the shape above ~15KB.** The capture checklist enforces this.
- **Prefer one larger unit with Checkpoints over two small ones.** If a unit's capture would be a single line, it is a Pass, or it belongs merged with its neighbour.
- **Several units per session is normal.** Each one is still agreed separately. Keep `Resume next session` accurate enough that a cold session can act from it without reading the whole shape.
- **Delegate mechanical work to a cheaper model tier**; keep orchestration, captures and Decision Slices in-context.
- **Archive closed shapes** to `~/.claude/shape-archive/{repo}/{date}-{feature}/`.
- **Don't solicit process moves.** Propose a Re-cut, a model re-check, or an extra validation round only when a trigger in the loop actually fired — not as a standing offer.

## Skill improvement

This skill is usage-informed but not self-mutating.

During product work, capture friction only as Skill Feedback (`assets/skill-feedback-template.md`): repeated confusion, missing template fields, unclear boundaries, too much ceremony, terminology that caused mistakes, or patterns the developer invented mid-flow because the skill didn't acknowledge them. That last one is the strongest signal — a section added to a shape file by hand probably belongs in the template.

Review feedback after the product shape is implemented or paused. Change this skill, its templates, or its examples only during an explicit skill-improvement Shape Pass. Suggest at most one or two focused improvements at a time.

## Output style

Compact and operational. A short Shape update, a short list of Candidate Slices, one recommended unit with its kind, direct capture notes after review. Be critical of over-planning, context bloat, vague abstractions, and drift. Skip methodology explanations unless asked.
