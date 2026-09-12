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
.agents/skills/shape-dd/        # Codex-compatible
.claude/skills/shape-dd/        # Claude Code, repo-local
~/.claude/skills/shape-dd/      # Claude Code, user-level
```

The folder can also be installed as a user-level skill if your agent supports global skills.

## Files

```text
shape-dd/
  SKILL.md
  README.md
  assets/
    shape-template.md            # the Current Shape scaffold
    slice-template.md            # separate Slice records, for larger work
    skill-feedback-template.md   # process friction captured during real use
  examples/
    single-file-shape.md         # small task, one file
    feature-folder-shape.md      # larger task, shape + slices
    opening-response.md          # density target for the first reply
  references/
    sizing.md                    # read when a unit boundary feels off
    capture-formats.md           # read at the end of a Shape Pass
```

`SKILL.md` is loaded whenever the skill triggers; `references/` files are read on demand, so detail lives there rather than inflating the entry file.

## Suggested repo shape locations

Small task:

```text
docs/shapes/{task-name}-shape.md
```

Larger task:

```text
docs/shapes/{feature-or-task}-shape/
  shape.md
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
