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

## The skills

### `plan-kickoff` — planning cadence

Fires when a planning session starts. Its central bet: **most bad plans fail on an unverified premise, not on insufficient detail.**

So it asks for the premises first, ranked by how much of the plan collapses if each is wrong, and for a decisions table (choice / alternative rejected / consequence accepted) *before* any file-by-file instructions. That table is what a human reviews — reviewing instructions can only confirm a plan is internally consistent, which is how a wrong design gets more precise instead of getting fixed.

It also caps plan length on purpose. A long, precise plan is usually an unresolved model that got specified instead of decided.

### `shape-dd` — Shape-Driven Agentic Development

A lightweight anti-drift workflow sitting between vibe coding and spec-driven development. Rough Intent, a compact Current Shape, and one reviewable unit at a time.

The vocabulary is the point: work comes as a **Build Slice**, a **Decision Slice** (resolving an open question, no code required), a **Re-cut** (revising the slice list itself), or a **Pass** (smaller than a slice). Naming all four stops the agent forcing every step into a "write code" frame, and stops the plan changing silently.

"Anti-drift" doesn't mean stick to the plan. It means changing course is a deliberate, named, captured move.

Has its own [README](skills/shape-dd/README.md) with fuller detail.

### `journal` — session reflection

Captures how you and the agent actually worked together — reactions, redirects, friction — not what got built. Technical content rots as the codebase changes; how someone thinks about collaboration changes slowly, and that's the layer worth keeping.

Its most useful rule is the one about delivery: **a reflection nobody reads changes nothing.** When a lesson repeats, the skill pushes it into a skill or into persistent memory, because those get loaded and journal files don't.

## Install

Copy the folders into wherever your agent reads skills from:

```text
~/.claude/skills/<skill>/      # Claude Code, user-level
.claude/skills/<skill>/        # Claude Code, repo-local
.agents/skills/<skill>/        # Codex-compatible
```

`shape-dd` and `journal` are tool-agnostic in their mechanics. `plan-kickoff` describes structured multiple-choice prompts and a plan-approval step generically, so it degrades gracefully on agents that lack them.

## Making them yours

These encode one person's working preferences. That's a feature — the point is an agent that doesn't need to be told the same thing every week — but it means **the defaults are calibration, not law.**

`plan-kickoff` keeps its tunable values in a **Local calibration** section at the end, deliberately separated from the general rules. Edit that section freely; when the `journal` skill promotes a lesson about how *you* work, it lands there rather than rewriting the rules. That separation is what keeps the skill shareable while still absorbing what it learns.

`shape-dd` carries the same idea as a **Working Agreement** section in its shape template.

## A note on the journal directory

The `journal` skill writes to `~/.claude/journal/`, which accumulates candid notes about real work and real decisions. **Keep that directory out of any repository you publish.** The skill is shareable; the journal is not. This repo's `.gitignore` blocks it as a precaution.

## License

MIT. See [LICENSE](LICENSE).
