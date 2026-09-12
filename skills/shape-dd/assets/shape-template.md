# {Feature or Task} Shape

Status: Draft | Active | Paused | Done

## Intent

What are we trying to achieve, and why?

Keep this rough unless the work truly needs more detail.

## Working Agreement

How we will collaborate on this shape. Edit if needed; don't silently delete.

- Slice entries below are rough direction and validation targets, not prescriptive implementation plans. Exact scope of each unit is agreed in conversation just before building.
- Before each unit (Build Slice / Decision Slice / Re-cut / Pass): the agent restates intended scope and kind; the developer agrees, requests narrowing, or redirects.
- Before each unit, the agent also gives a short chat summary of the next step's goal, scale, boundary, and likely architecture impact, so the developer can orient without opening the shape file — and explicitly invites challenge to the approach before code work starts.
- If that summary surfaces tension with the developer's vision, architecture, or implementation approach, the flow pauses for discussion or a Decision Slice before code continues.
- After each unit: the agent shows the diff plus validation results and stops.
- The agent does not commit, push, or chain into the next unit without explicit developer approval. Even tightly related follow-on work is its own pass.

## Source Material

Optional. Link or summarize any existing plan, spec, issue, design note, or implementation outline used to seed this shape.

- 

## Current Shape

### Current understanding

- 

### Decisions

Load-bearing choices for current and future units. Prune at close: mark superseded entries `[superseded by …]` or move them to an archive section so live decisions are easy to find.

- 

### Constraints

- 

### Assumptions

- 

### Risks

- 

### Open questions

- 

### Pending validation

Units that are built but not yet verified. Move down to Completed units once validation lands. Empty when nothing is in flight — but check here on resume before assuming a "Completed" entry is fully verified.

- 

### Completed units

Running log of *built and validated* units. Each captured unit gets one entry (newest first or oldest first — pick one and stay consistent). Entries can be Build Slices, Decision Slices, Re-cuts, or Passes; tag the kind so future readers can scan the log.

- {date} - [Build Slice] {name}: actual change, validation result, key decisions/risks.
- {date} - [Decision Slice] {name}: question resolved, decision, options rejected, artifacts updated.
- {date} - [Re-cut] {name}: trigger, before/after of slice list, downstream effects.
- {date} - [Pass] {name}: what was corrected/polished/planned, validation, follow-up if any.

## Candidate Slices

1. 
2. 
3. 

## Selected Slice

These three sections (Selected Slice, Review Notes, Capture) describe the **current pass only**. When a Slice is captured, summarize it into Completed Slices above and reset these sections for the next pass.

Slice:

Goal:

Boundary:

Expected files/areas touched:

Validation:

## Review Notes

Actual change:

Validation result:

Issues or surprises:

## Capture

Update after each Shape Pass.

### Shape changes

- 

### New decisions

- 

### New or changed assumptions

- 

### New constraints or risks

- 

### Remaining open questions

- 

### Likely next Slices

1. 
2. 

### Skill Feedback

Capture only process/tooling friction, not product work.

- 

## Resume next session

Optional but high-value for shapes that span more than one session. Keep it short — a session resuming here should not need to read the whole shape to act.

**State on disk:** uncommitted changes, in-flight branches, anything not yet shipped.

**Canonical validation commands:** exact commands, queries, or curl invocations to verify the current slice (e.g. KQL queries, test commands, dev URLs). Reusable across sessions.

**First action:** the one thing to do on resume — usually commit something, validate something pending, or agree the next unit.
