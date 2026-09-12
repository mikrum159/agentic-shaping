# Agentic shaping

Three agent skills for keeping AI-assisted software work honest: one for planning, one for building, one for learning what actually worked.

They're separable, but they were built as a loop and they refer to each other. Installing all three costs little and closes the cycle.

```
plan-kickoff  →  shape-dd  →  journal
   plan a          build it        capture what you learned
   ↑                                       │
   └───────────────────────────────────────┘
             promoted back as rules
```

## What it looks like

You start with rough intent. The agent doesn't start coding, and it doesn't interview you either:

```text
> Add CSV export for the filtered invoice list.

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

Then before any code is touched, you get something you can judge without opening a file:

```text
Next: the export endpoint. Small — one route, one service call, one
integration test. Touches the invoice API and the filter service; leaves
the list endpoint's response contract alone. Commits to a dedicated
endpoint rather than overloading the list. Still the right next unit.
                                                          — Build Slice

Anything here you'd shape differently?
```

That second message is the whole bet. It costs one round trip; an over-stuffed slice that has to be rolled back costs far more.

## Who this is for

If you've tried spec-driven development — Spec Kit, BMAD, OpenSpec — and found the upfront specification heavier than the work it was protecting, this is the lighter thing. It assumes the plan will be wrong in ways you can't predict, and spends its rules on making course changes cheap and visible rather than on getting the spec right first.

Probably not for you if you want generated artifacts and automation (OpenSpec's delta tracking, GSD's subagent orchestration), a test-first discipline (Superpowers), or one process an entire team follows identically. These are instructions, not tooling. They change how an agent behaves in conversation, and they are calibrated to one person by design.

## The skills

### `plan-kickoff` — planning cadence

Fires when a planning session starts. Its central bet: **most bad plans fail on an unverified premise, not on insufficient detail.**

So it asks for the premises first, ranked by how much of the plan collapses if each is wrong, and for a decisions table (choice / alternative rejected / consequence accepted) *before* any file-by-file instructions. That table is what a human reviews — reviewing instructions can only confirm a plan is internally consistent, which is how a wrong design gets more precise instead of getting fixed.

It also caps plan length on purpose. A long, precise plan is usually an unresolved model that got specified instead of decided.

### `shape-dd` — Shape-Driven Agentic Development

A lightweight anti-drift workflow sitting between vibe coding and spec-driven development. Rough Intent, a compact Current Shape, and one reviewable unit at a time. **If you install only one of these, install this one.**

The vocabulary is the point: work comes as a **Build Slice**, a **Decision Slice** (resolving an open question, no code required), a **Re-cut** (revising the slice list itself), or a **Pass** (smaller than a slice). Naming all four stops the agent forcing every step into a "write code" frame, and stops the plan changing silently.

A fifth term does quieter work. A **Checkpoint** is a pause *inside* a unit — no agreement ritual, no capture, silence means proceed. It exists because correction opportunity and unit size are different knobs, and fusing them is what makes slices shrink until every one carries a full ceremony and the whole loop reads as overhead.

"Anti-drift" doesn't mean stick to the plan. It means changing course is a deliberate, named, captured move.

The shape splits state from history — `shape.md` stays small and readable, `log.md` accumulates. Since shape files usually aren't committed, a closed shape can be archived to `~/.claude/shape-archive/` before the branch disappears, taking the log and the accumulated process feedback with it.

Has its own [README](skills/shape-dd/README.md) with fuller detail.

### `journal` — session reflection

Captures how you and the agent actually worked together — reactions, redirects, friction — not what got built. Technical content rots as the codebase changes; how someone thinks about collaboration changes slowly, and that's the layer worth keeping.

Its trigger is **divergence**: the plan bent, two options were argued, a decision got reversed. A session that ran straight down an agreed plan gets no entry, however much got built. That's also what separates it from auto-memory — memory stores the conclusion, the journal stores the argument.

Its most useful rule is the one about delivery: **a reflection nobody reads changes nothing.** When a lesson repeats, the skill pushes it into a skill or into persistent memory, because those get loaded and journal files don't.

## Install

**As a plugin (Claude Code) — recommended.** This repo is also a plugin marketplace, so every machine installs from the same source and `git pull` is the sync mechanism:

```text
/plugin marketplace add mikrum159/agentic-shaping
/plugin install agentic-shaping@mikrum159-skills
```

Try it from a local clone first with `/plugin marketplace add ./agentic-shaping`. Later changes arrive via `/plugin marketplace update mikrum159-skills`.

**By copying**, for a single machine or another agent:

```text
~/.claude/skills/<skill>/      # Claude Code, user-level
.claude/skills/<skill>/        # Claude Code, repo-local
```

Each skill is a self-contained folder — copy it wherever your agent reads skills from.

`shape-dd` and `journal` are tool-agnostic in their mechanics; only their file paths assume a `~/.claude/` home. `plan-kickoff` describes structured multiple-choice prompts and a plan-approval step generically, so it degrades gracefully on agents that lack them.

## Making them yours

These encode one person's working preferences. That's a feature — the point is an agent that doesn't need to be told the same thing every week — but it means **the defaults are calibration, not law.**

Both `plan-kickoff` and `shape-dd` keep their tunable values in a **Local calibration** section, deliberately separated from the general rules: plan length ceilings and question batch sizes in one, commit policy and preferred unit size in the other. Edit those freely. When the `journal` skill promotes a lesson about how *you* work, it lands there rather than rewriting the rules — and that separation is what keeps a skill shareable while it absorbs what it learns.

`shape-dd`'s shape template also has a **Working Agreement** section, but only for what differs on one particular shape. Standing preferences belong in the skill, so they aren't re-litigated every time a shape is created.

## A note on the journal directory

The `journal` skill writes to `~/.claude/journal/`, which accumulates candid notes about real work and real decisions. **Keep that directory out of any repository you publish.** The skill is shareable; the journal is not. This repo's `.gitignore` blocks it as a precaution.

## License

MIT. See [LICENSE](LICENSE).
