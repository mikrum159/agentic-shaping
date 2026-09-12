# {Feature or Task} — Log

Append-only history for `shape.md`. Never rewritten, only added to. This is the record worth archiving when the shape closes.

For a single-file shape, paste these sections at the bottom of the shape file instead of keeping a separate log.

## Completed units

Built *and validated* units, newest first (or oldest first — pick one and stay consistent). Tag the kind so the log can be scanned.

- {date} — [Build Slice] {name}: actual change, validation result, key decisions/risks.
- {date} — [Decision Slice] {name}: question resolved, decision, options rejected, artifacts updated.
- {date} — [Re-cut] {name}: trigger, before/after of the slice list, downstream effects.
- {date} — [Pass] {name}: what was corrected/polished/planned, validation, follow-up.

Capture grows with how surprising the unit was: a fully-predicted unit gets a line or two; a mid-flight correction, an unexpected blocker, or an off-plan decision deserves a paragraph. The surprise is the load-bearing content for future sessions.

## Interim progress

Checkpoints appended during a long or multi-session unit, so early detail isn't lost by the time it ends. Fold into the unit's Completed entry on capture, or leave in place if the detail is worth keeping.

- {date} — {unit}: what landed, what's next inside the boundary, anything found that might change the plan.

## Skill Feedback

Process and tooling friction only — not product work. Survives to the archive, where the skill-improvement pass reads it.

Use `skill-feedback-template.md` for anything needing more than a line.

- {date} — {friction observed}: what it caused, suggested change.

## Closure summary

Filled in when Status flips to `Closed`, and read by `references/archiving.md` when the shape is archived.

**Shipped:**

**Deferred, and where it went:**

**Successor shape:**

**Related reflections:** any `~/.claude/journal/reflections/` entries from this shape's run — where the plan was argued, reversed, or found wrong. Leave empty if none.
