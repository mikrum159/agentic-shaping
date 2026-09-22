# Delegating a unit to a sub-agent

Read this before writing a brief.

## What to delegate

Delegate when **both** hold:

- the unit is self-contained enough that a one-shot brief describes it fully — no live conversational context needed,
- it is mechanical or well-bounded enough that briefing costs less than doing.

Keep it direct when the unit is one line, judgment-heavy, or depends on context already loaded. Captures and Decision Slices are never delegated — they depend on full conversation state and judgment.

Delegate by default: mechanical renames across files, doc and text sweeps, build/test verification runs, bounded research and codebase exploration.

Rule of thumb from practice: a single-line change is faster done directly — briefing overhead outweighs the saving. A 3-file rename or a 15-edit doc sweep is worth the brief.

## Model tiering

Match the model tier to the judgment the work requires. A capable model orchestrates; a mid tier handles bounded code edits and verification; the cheapest tier handles mechanical doc/text sweeps and research. Use whatever capable/cheaper split the agent supports — the tiering matters more than the names.

## The brief

Four parts:

1. **Background** — what shape, what unit, why this change.
2. **In-scope changes** — exact files, exact edits.
3. **Out of boundary — do not touch** — the highest-value section. An explicit list is what prevents scope creep.
4. **Verification and report-back** — the build/grep/test step, and the format results should come back in.

Cover ambiguous edge cases explicitly. A sub-agent has no chat context and will interpret narrowly.

## Handing the next session to a cheaper model

Sometimes a whole session goes to a cheaper model rather than one unit to a sub-agent. Then the shape itself is the brief. Before handing over, run a Pass that audits `Resume next session` and the next Candidate Slice for:

- **Undecided forks.** Two reasonable ways to wire something, with no choice recorded.
- **Rules with no mechanism.** "Pin versions" with nothing saying how.
- **Loose scope.** A boundary that invites over-building.
- **Standing rules the model may never see.** A session that doesn't load the skill never reads Local calibration. Copy the ones that matter, such as never committing, into the Working Agreement.

## Trust but verify

Read the diff and re-run validation yourself before accepting the result. A delegated unit still goes through the normal review and capture steps — delegation changes who types, not who is accountable.
