# Example opening response

When the user provides rough Intent, match this density. Long methodology recaps are noise.

```text
Intent: Add CSV export for the filtered invoice list.

Current Shape (new):
- Reuse existing list filters; export endpoint, not list overload.
- Out of scope: UI polish, new reporting framework.

Candidate Slices:
1. Backend export endpoint reusing list filters (+ test).
2. UI export button wired to current filter state.
3. Filename/date formatting and edge cases.

Selected unit: Build Slice 1. Stopping here for confirmation before building.
```

The shape of a good opening:

- one or two sentences restating Intent
- 2-4 bullets sketching the Current Shape (just enough to anchor scope and call out out-of-scope items)
- 2-4 Candidate Slices, terse
- one recommended Selected unit with kind named, and an explicit pause for agreement

Avoid: full methodology recap, multi-section headers, exhaustive constraints/assumptions/risks lists on a small shape. Those belong in the shape file itself, not the opening message.
