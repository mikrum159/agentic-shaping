# Capture formats per unit kind

Read this at the end of a Shape Pass when deciding what to write into the shape file. The capture format depends on what kind of unit just finished.

A unit is not fully captured until validation has landed. If a Build Slice was built but not yet validated, keep it under a **Pending validation** subsection of the shape, not under Completed units. Move it down once validation has passed and the entry is final.

## Build Slice capture

- completed slice
- actual change made (files touched, key choices)
- validation result (or "pending validation" with what's blocking)
- new or changed decisions / assumptions / constraints / risks
- open questions surfaced
- likely next units

## Decision Slice capture

- resolved question(s)
- decision and short rationale
- options considered, with reasons for rejection
- artifacts updated (shape Decisions, spec docs, slice list)
- validation: how we know the decision is consistent (e.g. "every field in the snapshot now has a named provenance")

## Re-cut capture

- trigger (what new information drove this)
- before/after of the relevant part of the slice list
- rationale per change (split / insert / reorder / drop)
- downstream effects (validation criteria changed, blocked questions cleared)

## Pass capture

- what the pass corrected, polished, or planned
- validation (often lighter than a Slice)
- whether it surfaces follow-up

## Sizing the capture

Capture grows with how surprising the unit was. A fully-predicted Build Slice that matched the agreed boundary gets one or two lines. A unit with a mid-flight architectural correction, an unexpected blocker, or a decision that wasn't on the slice list deserves a paragraph — the surprise *is* the load-bearing content for future sessions.
