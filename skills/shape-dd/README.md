# shape-dd

`shape-dd` is a reusable agent skill for Shape-Driven Agentic Development, also called Agentic Sculpting.

It helps AI coding agents keep work aligned through:

- rough Intent or existing plan material
- compact Current Shape
- one reviewable Slice at a time
- developer-agent clarification around decisions that matter
- review and capture after every Shape Pass
- explicit skill feedback after real usage

## Install

Copy this folder into the skill location used by your agent.

Common repo-local locations:

```text
.claude/skills/shape-dd/        # Claude Code, repo-local
~/.claude/skills/shape-dd/      # Claude Code, user-level
```

The folder is self-contained, so it also drops into whatever directory another agent reads skills from. The mechanics are tool-agnostic; only the archive path assumes a `~/.claude/` home.

The whole repo also installs as a plugin — see the [root README](../../README.md).

## Files

```text
shape-dd/
  SKILL.md
  README.md
  assets/
    shape-template.md            # current state — what a cold session reads
    log-template.md              # append-only history, split out of the shape
    slice-template.md            # separate Slice records, for larger work
    skill-feedback-template.md   # process friction captured during real use
  examples/
    single-file-shape.md         # small task, state + log in one file
    feature-folder-shape.md      # larger task, shape.md + log.md
    opening-response.md          # density target for the first reply
  references/
    sizing.md                    # read when a unit boundary feels off
    capture-formats.md           # read when a unit is shown, and on acceptance
    delegation.md                # read before briefing a sub-agent
    archiving.md                 # read when closing a shape out before a PR
```

`SKILL.md` is loaded whenever the skill triggers and stays in context across turns, so every line is a recurring cost. `references/` files are read on demand — detail lives there rather than inflating the entry file.

The shape splits **state** from **history**: `shape.md` holds what is true now and stays small; `log.md` accumulates captures and is never rewritten. A small task keeps both in one file.

## Suggested repo shape locations

Small task:

```text
docs/shapes/{task-name}-shape.md
```

Larger task:

```text
docs/shapes/{feature-or-task}-shape/
  shape.md
  log.md
  slices/
    001-{slice-name}.md
```

Use the single-file shape until the work clearly needs more structure.

## Existing plans

An existing `plan.md`, issue, spec, design note, or implementation outline can seed a shape.

The skill should distill that source material into Intent, Current Shape, assumptions, risks, Candidate Slices, and a recommended next Slice. The plan may remain a reference, but active work still proceeds through Shape Passes.

## Developer-agent loop

The agent should preserve developer intent, ask only questions that materially affect the next Slice, state safe assumptions, point out risks or conflicts, and suggest narrower Slices when work is too broad or risky.

## Example invocations

```text
Use shape-dd to initialize a shape for this intent: ...
```

```text
Use shape-dd to distill this plan.md into a Current Shape and propose the first Slice.
```

```text
Use shape-dd to propose the next Slice from docs/shapes/payment-retry-shape.md.
```

```text
Use shape-dd to review this completed Slice and update the Current Shape.
```

```text
Use shape-dd to review captured Skill Feedback and propose one improvement to the skill.
```

## Version stance

This skill is usage-informed but not self-mutating.

During product work, capture process friction as Skill Feedback. Change `SKILL.md`, templates, or examples only during an explicit skill-improvement Shape Pass.
