# Account Merge Shape

Status: Active

Workflow: shape-dd. Load the skill before acting on this file.

Example of the **folder** form, at the start of the work. This file is `shape.md` — state only. History goes to `log.md` beside it.

```text
docs/shapes/account-merge-shape/
  shape.md    # this file — current state
  log.md      # append-only history, from assets/log-template.md
  slices/     # optional, for units that need their own record
```

## Resume next session

**First action:** agree the boundary for the data inventory unit and start it.

**State on disk:** nothing yet — shape just created.

**Canonical validation commands:** none yet; the first unit is investigation.

## Intent

Allow support staff to merge duplicate customer accounts safely, preserving auditability and avoiding accidental data loss.

## Working Agreement

Nothing differs from the skill's Local calibration.

## Source Material

- Existing support workflow notes describe the duplicate-account pain but do not define merge rules.

## Current Shape

### Current understanding

- Account data spans profile, billing, notes, and login identity.
- The risky part is not the button; it is defining a safe merge boundary.

### Decisions

- Start with a read-only merge preview before any write operation.
- Capture unresolved domain rules rather than guessing them.

### Constraints

- Must preserve audit history. *(from `docs/support/audit-policy.md` — verified against the code, audit rows are append-only)*
- Must not merge authentication identities in the first implementation pass. *(developer)*
- Must not change billing ownership without explicit product/domain review. *(from the support workflow notes — **unverified**, notes are 2 years old; confirm before it blocks a unit)*

### Assumptions

- Support staff need visibility into conflicts before any merge action is offered.

### Risks

- Merge rules may differ by data area and cannot be inferred from table names alone.
- A write operation before preview review could cause irreversible data loss.

### Open questions

- Which account fields win on conflict?
- Who is allowed to perform merges?
- What undo or rollback expectation exists?

### Pending validation

- None.

## Candidate Slices

Rough direction, not a plan of record. The conflict-rule questions above may force a Decision Slice before slice 2.

1. Inventory account-related data; classify merge-safe vs blocked areas.
2. Read-only merge preview model.
3. Tests for preview conflict detection.
4. Minimal support-staff UI, preview only.

## Current unit

Unit: Account data inventory — Build Slice

Goal: Produce a compact map of account-related data, classifying what can be previewed, merged later, or blocked.

Boundary: Investigation and documentation only. No production code changes.

Expected files/areas touched:

- This shape file, plus links to existing docs if any are found.

Validation:

- Account-related modules and tables are identified.
- Unknowns are captured as open questions rather than guessed.
- The preview model unit can start without guessing.

### Review notes

Actual change:

Validation result:

Issues or surprises:
