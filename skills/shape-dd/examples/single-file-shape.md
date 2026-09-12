# Invoice CSV Export Shape

Status: Active

## Intent

Add a simple CSV export for the invoice list so users can download the currently filtered results for offline reporting.

## Source Material

- None. This shape started from rough intent.

## Current Shape

### Current understanding

- The invoice list already supports filtering by date, status, and customer.
- Export should reuse the same filter state as the visible list.
- The first pass should focus on backend/API behavior, not UI polish.

### Decisions

- CSV export will be a dedicated endpoint rather than overloading the list endpoint.
- The first Slice will include a small integration test for filter reuse.

### Constraints

- Do not redesign invoice filtering.
- Do not introduce a reporting framework.
- Keep CSV columns limited to fields already visible in the list.

### Assumptions

- Existing invoice query/filter logic can be reused for export.
- CSV columns should initially match fields already visible in the invoice list.

### Risks

- Export behavior could drift from list behavior if it uses separate filtering logic.
- UI work could expand the first Slice beyond the backend validation boundary.

### Open questions

- Exact filename convention can be decided later.

### Completed Slices

- None.

## Candidate Slices

1. Add backend export endpoint using existing filters.
2. Add UI export button wired to current filter state.
3. Add filename/date formatting and edge-case polish.

## Selected Slice

Slice: Add backend export endpoint using existing filters.

Goal: Provide a CSV response for invoices matching the same filter inputs as the list endpoint.

Boundary: API route, export handler/service, and tests only. No UI work.

Expected files/areas touched:

- Invoice API/controller
- Invoice query/filter service
- CSV serialization helper if needed
- API/integration tests

Validation:

- Existing invoice list tests still pass.
- New test proves status/date/customer filters affect export output.
- CSV response includes expected headers and visible-list fields.

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

- Filename convention.

### Likely next Slices

1. Add UI export button.
2. Add filename/date formatting.

### Skill Feedback

- None yet.
