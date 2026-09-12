# Sizing each kind of unit

Read this when proposing a Selected unit and the boundary feels off.

## Checkpoint before you split

The default is **one larger unit with Checkpoints**, not two small ones. A unit that is correctly sized but *long* doesn't need cutting — it needs a pause partway through.

Split only when the validations are genuinely unrelated. Checkpoint when there is one validation and the developer would simply like a look before it lands.

Fusing correction opportunity to unit size is what drives slices to shrink: if the only way to get another look is to cut another Slice, slices get cut smaller and smaller until every one carries a full agree → build → show → capture ceremony, and the loop reads as overhead.

## Build Slice

One reviewable change: one concern, one validation criterion, one rollback unit. Roughly PR-sized.

The test is whether you can state the boundary in one sentence and a reviewer can judge it against a single goal — not file count. A scaffold Build Slice that creates 20 files is fine; a 3-file change mixing auth and routing is not.

**Floor:** if the unit's capture would be a single line, it is too small to be a Slice. Make it a Pass, or merge it into the neighbouring unit.

**Ceiling:** if it needs multiple unrelated validations, or its boundary is hard to state in one sentence, it is probably two units — after you've ruled out a Checkpoint.

## Decision Slice

Resolves one named question. Its validation is consistency: every claim it makes can be defended against the prior Current Shape and against any new evidence cited.

## Re-cut

Explains what changed in the slice list and why, with a clear before/after of the affected entries. It is its own unit, never a side effect of another one.

## Pass

Small enough that it doesn't deserve a row in the slice list, big enough to deserve its own capture rather than being folded into the next unit's notes. Polish, chrome, planning, and narrow corrections all qualify.
