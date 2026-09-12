# Capture formats per unit kind

Read this at the end of a Shape Pass, and whenever the developer asks any version of *"anything to update before I commit?"* — that question means close the pass, not just append notes.

## End-of-pass checklist

Run all five. Steps 3 and 4 are the ones most often skipped, and skipping them is what leaves a finished unit reading as still open in the next session.

1. **Write the capture** in the log, using the format for the unit's kind below.
2. **Move the unit** out of `Pending validation` in the shape file, into the log's `Completed units` — only if validation has actually landed. If it hasn't, leave it in `Pending validation` and say what's blocking.
3. **Reset `Current unit`** in the shape file, including its Review notes. A captured unit must not still be sitting there.
4. **Update `Resume next session`** — first action, state on disk, validation commands. This is what the next session reads first.
5. **Update the live state** that changed: Decisions, Constraints, Assumptions, Risks, Open questions, Candidate Slices.

A unit is not captured until validation has landed. Built-but-unvalidated work stays under `Pending validation`, never under Completed units — otherwise a future session reads "Completed" as verified when some entries are merely built.

## Build Slice

- actual change made (files touched, key choices)
- validation result, or "pending validation" with what's blocking
- new or changed decisions / assumptions / constraints / risks
- open questions surfaced
- likely next units

## Decision Slice

- question(s) resolved
- decision and short rationale
- options considered, with reasons for rejection
- artifacts updated (Decisions, spec docs, slice list)
- validation: how we know the decision is consistent (e.g. "every field in the snapshot now has a named provenance")

## Re-cut

- trigger — what new information drove this
- before/after of the affected part of the slice list
- rationale per change (split / insert / reorder / drop)
- downstream effects: validation criteria changed, blocked questions cleared

## Pass

- what the pass corrected, polished, or planned
- validation, often lighter than a Slice
- whether it surfaces follow-up

## Sizing the capture

Capture grows with how surprising the unit was. A fully-predicted unit that matched its agreed boundary gets one or two lines. A unit with a mid-flight architectural correction, an unexpected blocker, or a decision that wasn't on the slice list deserves a paragraph — the surprise *is* the load-bearing content for future sessions.

On a long or multi-session unit, append checkpoints to the log's `Interim progress` as you go. One consolidated capture works for a same-day unit; on a multi-day one the early detail is usually lost by the end.
