# Invoice CSV Export Shape

Status: Active

Example of the **single-file** form: state first, log sections appended at the bottom. One unit is done, the next is agreed.

## Resume next session

**First action:** agree the boundary for the UI export button, then build it.

**State on disk:** working on `feature/invoice-export`, local only and not yet pushed.

**Canonical validation commands:** `npm test -- invoices`, and `curl localhost:3000/api/invoices/export?status=paid` for a manual check.

## Intent

Add a simple CSV export for the invoice list so users can download the currently filtered results for offline reporting.

## Working Agreement

Nothing differs from the skill's Local calibration.

## Source Material

- None. Started from rough intent.

## Current Shape

### Current understanding

- The invoice list already supports filtering by date, status, and customer.
- Export reuses the same filter state as the visible list.
- Backend landed first; UI is next.

### Decisions

- CSV export is a dedicated endpoint rather than an overload of the list endpoint.
- CSV columns match fields already visible in the invoice list.

### Constraints

- Do not redesign invoice filtering. *(developer)*
- Do not introduce a reporting framework. *(developer)*

### Assumptions

- The existing invoice query/filter logic is reusable for export.

### Risks

- Export behavior could drift from list behavior if the two ever stop sharing filter logic.

### Open questions

- Filename convention — deferred to the polish unit.

### Pending validation

- None.

## Candidate Slices

Rough direction, not a plan of record.

1. ~~Backend export endpoint reusing existing filters.~~ Done.
2. UI export button wired to current filter state.
3. Filename/date formatting and edge cases.

## Current unit

Unit: UI export button — Build Slice

Goal: Let the user trigger the export from the invoice list, using whatever filters are currently applied.

Boundary: Invoice list component and its tests only. No changes to the endpoint, no filename work.

Expected files/areas touched:

- Invoice list component
- Component tests

Validation:

- Clicking export with active filters requests the endpoint with those same filter params.
- Existing invoice list tests still pass.

### Review notes

Actual change:

Validation result:

Issues or surprises:

---

# Log

## Units

- 2026-03-04 — [Build Slice] 1. Backend export endpoint: added `GET /api/invoices/export` reusing `InvoiceFilterService`, plus a CSV serialization helper. Integration test proves status/date/customer filters change export output; existing list tests pass. Decision: dedicated endpoint, not a list-endpoint overload — keeps the list response contract untouched. Status: validated

## Skill Feedback

- None yet.
