# 2026-03-14 — checkout retry policy

> Example reflection. Fictional, included with the skill as a tone reference.
> Note what it does: names concrete mechanisms, records a silent acceptance,
> and the Change section criticises the agent rather than the user.

## Subject
Planning session: designing a retry policy for failed checkout payments. Most of the value was in narrowing scope, not in the design itself.

## How I iterated
- Opened with the problem, not a spec — "payments fail and we drop them on the floor, what are our options?"
- Took three prose options before any structured question. Rejected the queue-based one immediately as "too much machinery for the volume we have."
- Added a constraint in turn three that wasn't in the brief: retries must not fire after the customer has already been emailed a failure notice. That reshaped the whole timing model.
- Went terse once the direction was agreed — "yes, do that" — and stayed terse through the plan draft.

## Reactions
- **Liked:** being shown the cost of each option in the same breath as the option. The "this needs a scheduler, that doesn't" framing settled it in one turn.
- **Pushed back on:** the proposed exponential backoff. "Our payment provider rate-limits at a fixed window, so backoff buys nothing" — the agent had assumed a generic API without checking the provider docs.
- **Silently accepted:** capping retries at 3, dropping the admin-visible retry log to a follow-up, and putting the plan in `docs/` rather than the issue tracker.

## Keep doing
- Read the actual provider/library docs before proposing a policy that depends on their behaviour. The backoff mistake came from a generic assumption.
- Price each option as it's offered — the option list is only useful when the trade-off is attached.
- Stop at the plan. No code was written this session and that was right.

## Change
- I proposed exponential backoff because it's the standard answer, not because it fit this system. Standard answers still need a reason to apply here.
- I asked which retry count to use before establishing whether retries were time-bounded at all. Wrong order — the bound determined the count.

## Open threads
- Whether failed retries should surface in the admin UI or only in logs. Deferred, not decided.
- The email-notice timing constraint probably affects the refund flow too. Not investigated.
