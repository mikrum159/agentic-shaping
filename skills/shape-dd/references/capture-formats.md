# Capture formats per unit kind

Read this when a unit is shown, and again on **acceptance**: when the developer asks any version of *"validated, staged — anything to record?"*. That message means close the unit in the same reply, not just append notes.

## One entry per unit, with a status line

Write the unit's entry in the log's `Units` when it is shown, while the detail is fresh. End it with a status line:

- `Status: validated` — all of its validation has landed
- `Status: manual check open — <the check>` — built and shown; the developer still owns a check
- `Status: unconfirmed — <the check>` — the developer skipped the question on resume. The close audit re-checks it.

Later events **append a line to the same entry**. They are never new units:

- `Review round N — <feedback> → <what changed>` — feedback on a shown, unaccepted unit
- `Accepted <date> — "<developer's words>"` — then change the status to `validated`

`Pending validation` in the shape file indexes the entries whose status isn't `validated`. The log holds the record; Pending validation holds the list of what is still open.

## Writing a manual check

A manual check is only as good as its wording. On MarkScope, the check that mattered (a real restart) was the one never run, and another asked for something that could not happen. The checks that worked made the developer use the app in a way ordinary use doesn't. Write each one to:

- **Give steps and an observation.** Name what to do and what to look for, not just a feature to confirm.
- **Include the path ordinary use skips.** A restart, an error, large input, or repeating an action quickly.
- **Be reachable.** Before asking, confirm the observation can actually happen in the current build.

## Log format

One fixed format, so the log can be counted and scanned:

- **Order:** oldest first. Always append at the end; never insert an entry mid-log, even a late one.
- **Tag:** `[Build Slice] 17. Name` or `[Decision Slice] 3. Name`, using the Candidate Slice number. Passes and Re-cuts have no row in the slice list, so they take no number: `[Pass] Name`, `[Re-cut] Name`.
- **Validation line:** record the result against the canonical commands (e.g. "gate 120/120"), plus only what deviated. Don't restate the commands or their standing warnings in every entry.

## End-of-pass checklist

Run all six **on acceptance**. When the unit is first shown, run only step 1 and add the unit to `Pending validation`. Steps 3 and 4 are the ones most often skipped, and skipping them is what leaves a finished unit reading as still open in the next session.

1. **Write or complete the entry** in the log, using the format for the unit's kind below, with its status line.
2. **Update `Pending validation`.** Remove the unit once its status is `validated`. If a check is still open, leave the unit there and say what is blocking.
3. **Reset `Current unit`** in the shape file, including its Review notes. A captured unit must not still be sitting there.
4. **Update `Resume next session`**: first action, state on disk, validation commands. This is what the next session reads first.
5. **Update the live state** that changed: Decisions, Constraints, Assumptions, Risks, Open questions, Candidate Slices.
6. **Compact if needed.** Compact if `shape.md` is over the size threshold in Local calibration, or if any section only grew this pass. Fold finished detail into the log and strike through what has been superseded.

**Reset means replace.** Rewrite `Current unit` and `Resume next session` from scratch. Never append "On top of that…" to what is there. Appending is how a shape ends up with eight finished units in its Current unit.

**Never record commit state.** `State on disk` holds only what git cannot show. Whether the work is committed is read from git on resume.

On acceptance, also:
- quote the developer's words in the `Accepted` line
- tell them in one line which manual checks you recorded as passed on their word, so they can object without another round
- if the shape files are tracked in git, remind them to stage those files again

Acceptance is what closes a developer-owned check. A later commit found on resume does not close it: see Resume step 3 in `SKILL.md`.

## Build Slice

- actual change made (files touched, key choices)
- validation result, and the status line
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
