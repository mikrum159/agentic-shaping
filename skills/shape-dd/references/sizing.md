# Sizing each kind of unit

Read this when proposing a Selected unit and you're unsure whether the boundary is right.

A **Build Slice** should feel like one reviewable change: one concern, one validation criterion, one rollback unit. Roughly PR-sized. The right test is whether you can state the boundary in one sentence and a reviewer can judge it against a single goal — not the file count. A scaffold Build Slice that creates 20 files is fine; a 3-file change that mixes auth and routing is not.

A **Decision Slice** should resolve one named question. Its "validation" is consistency: every claim it makes can be defended against the prior Current Shape and against any new evidence cited.

A **Re-cut** should explain what changed in the slice list and why, with a clear before/after snapshot of the affected entries. It is itself a unit, not a side effect of another unit.

A **Pass** should be small enough that it doesn't belong as its own row in the slice list, but big enough to deserve a Capture entry instead of being folded into the next Slice's notes. Polish passes, chrome passes, planning passes, narrow correction passes all qualify.

If a unit needs multiple unrelated validations, or its boundary is hard to state in one sentence, it is probably two units.

**Before splitting, check whether you actually want a Checkpoint.** A Slice that is correctly sized but *long* doesn't need cutting — it needs a pause partway through. Split when the validations are genuinely unrelated; checkpoint when there's one validation and the developer would simply like a look before it lands.
