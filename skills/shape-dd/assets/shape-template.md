# {Feature or Task} Shape

Status: Draft | Active | Paused | Closed

This file holds **current state only** — what a cold session needs to act. Completed work lives in the log (`log.md`, or the appended Log sections at the bottom of this file for a single-file shape).

## Resume next session

Keep this accurate enough that a session resuming here can act without reading the rest of the file. On every capture, **replace** this section rather than appending to it.

**First action:** the one thing to do on resume — usually close out a pending unit, validate something, or agree the next unit.

**State on disk:** only what `git status` / `git log` cannot show. Examples: generated or gitignored files, local-only branches, a pushed but unmerged PR, where this shape lives if it isn't tracked. Never record whether the work is committed; read that from git on resume.

**Canonical validation commands:** exact commands, queries, or URLs to verify the current unit. Reusable across sessions.

## Intent

What are we trying to achieve, and why? Keep this rough unless the work truly needs more detail.

## Working Agreement

Standing defaults live in the skill's **Local calibration** section. Record here only what differs *for this shape* — a different commit policy, an autonomous stretch, a validation rule specific to this work. Delete the examples below if nothing differs.

- 

## Source Material

Optional. Link or summarize any existing plan, spec, issue, design note, or outline used to seed this shape.

- 

## Current Shape

### Current understanding

- 

### Decisions

Load-bearing choices for current and future units. Strike through rather than delete when superseded; prune at close.

Note the source of each — developer, code, or a document (with path). A decision inherited from documentation is only as current as that document.

If the repo keeps ADRs, a decision recorded there is one line plus the link. Don't restate its rationale here.

- 

### Constraints

Note the source of each, the same way. A constraint taken from a document is a claim until verified — the document may be out of date, and a stale one reads exactly like a real limit.

- 

### Assumptions

- 

### Risks

- 

### Open questions

- 

### Pending validation

An index of the log entries whose status is not yet `validated`: `manual check open` or `unconfirmed`. Name the check. Remove an item on acceptance. Empty when nothing is in flight. Check here on resume, before assuming anything is done, and never close an item because a commit appeared.

- 

## Candidate Slices

Rough direction and validation targets, **not** a plan of record. Nothing here is mandatory; each entry is re-evaluated when it comes up.

1. 
2. 
3. 

## Current unit

Describes the **current pass only**. On capture, summarize into the log and reset this section.

Unit: {name} — Build Slice | Decision Slice | Re-cut | Pass

Goal:

Boundary:

Expected files/areas touched:

Validation:

### Review notes

Actual change:

Validation result:

Issues or surprises:
