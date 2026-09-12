# Account Merge Shape

Status: Active

## Intent

Allow support staff to merge duplicate customer accounts safely while preserving auditability and avoiding accidental data loss.

## Source Material

- Existing support workflow notes described duplicate account pain, but did not define merge rules.

## Current Shape

### Current understanding

- Account data is spread across profile, billing, notes, and login identity areas.
- The risky part is not the button; it is defining a safe merge boundary.
- Work should proceed in narrow Slices with validation after each pass.

### Decisions

- Start with a read-only merge preview before any write operation.
- Treat destructive or irreversible changes as out of scope until preview behavior is reviewed.
- Capture unresolved domain rules rather than guessing.

### Constraints

- Must preserve audit history.
- Must not merge authentication identities in the first implementation pass.
- Must not change billing ownership without explicit product/domain review.

### Assumptions

- Support staff need visibility into conflicts before any merge action is offered.
- Existing account modules can be inspected before deciding the final write model.

### Risks

- Merge rules may differ by data area and cannot be safely inferred from table names alone.
- A write operation before preview review could create irreversible data loss.

### Open questions

- Which account fields win on conflict?
- Who is allowed to perform merges?
- What undo or rollback expectation exists?

### Completed Slices

- None.

## Candidate Slices

1. Inventory account-related data and identify merge-safe vs blocked areas.
2. Build read-only merge preview model.
3. Add tests for preview conflict detection.
4. Add minimal support-staff UI for preview only.

## Selected Slice

Slice: Inventory account-related data and identify merge-safe vs blocked areas.

Goal: Produce a compact map of account-related data and classify what can be previewed, merged later, or blocked.

Boundary: Investigation and documentation only. No production code changes.

Expected files/areas touched:

- Shape file only, unless existing docs need links.

Validation:

- Account-related modules/tables/files are identified.
- Unknowns are captured as open questions.
- Next Slice can build a preview model without guessing.

## Review Notes

Actual change:

- Pending.

Validation result:

- Pending.

Issues or surprises:

- Pending.

## Capture

Update after the Shape Pass.

### Shape changes

- Pending.

### New decisions

- Pending.

### New or changed assumptions

- Pending.

### New constraints or risks

- Pending.

### Remaining open questions

- Pending.

### Likely next Slices

1. Build read-only merge preview model.
2. Add tests for preview conflict detection.

### Skill Feedback

- None yet.
