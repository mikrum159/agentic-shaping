---
name: plan-kickoff
description: Light-touch guidance for planning sessions. Use when the user opens in plan mode or with framing like "let's plan X", "high-level ideas first", "turn this PoC into a real X", or any signal that they want shape and validation before code. Do NOT use for bug fixes, small refactors, or sessions where the plan is already approved.
---

# Plan kickoff

Keeps the cadence right in a planning session so the person you're working with doesn't have to restate how they want to work every time.

## How planning sessions go

Planning conversations are exploratory. Expect rich framing and directional opinions up front, and expect new requirements to surface in turn two or three — that's normal, not a failure of the initial brief. Your job is to make the plan flex to new information, not to extract everything upfront.

Default to thinking out loud with them rather than interrogating them.

## The rules

1. **Surface your assumptions, don't ask for them.** Before drafting, state in a short bullet list what you're assuming is out of scope, what variants you're accounting for, what write-actions are deferred, what data you can't show. They react and correct. This is a *list*, not a questionnaire.

   Then, separately and more importantly: **name the premises the design rests on that you could not verify** — facts about the environment, the data, the deployment, existing usage. Rank them by how much of the plan collapses if they're wrong, and phrase each so it costs one line to answer:

   > *Assumed: this table holds live data that must survive a rolling deploy. Unverified. If false, drop the nullable field, the legacy fallback and the storage/entity name split — roughly 40% of this plan.*

   A premise buried in the plan's prose never gets challenged. The same premise stated as a ranked question gets answered in seconds. This is the highest-leverage thing you do in a planning session.

2. **Discuss directions in prose before structured questions.** Propose 2–3 directional options conversationally, with a recommendation and why. Once the axes are clear, lock decisions via a structured multiple-choice prompt if your agent has one — batched, recommendations first, never one question at a time. People reframe faster against prose than against multiple-choice.

3. **Structure plans for change.** Leave open scaffolding in the first draft so new requirements land as local edits, not rewrites. Examples: a "variants" section even if you only know one variant; an explicit "out of scope (v1)" list that's easy to move items in or out of; phase boundaries that don't bake assumptions about phase 2+ detail.

4. **Phase multi-day work, expand only phase 1.** Phases 2+ get a name and one-line scope. Say it's skeleton, expand on request. Avoids over-investing in detail that shifts once phase 1 lands.

   The same instinct applies to the plan as a whole: **if it can't be stated in ~150 lines, the design isn't settled.** Length is not thoroughness — a long, precise plan is usually an unresolved model that got specified instead of decided. When it runs long, ask what could be *decided* rather than described.

5. **Lead the plan with a decisions table, not with instructions.** Before any file-by-file detail, list the 3–8 choices the design hinges on — one row each: the decision, the alternative rejected, the consequence being accepted. That table is the review surface; the instructions are downstream of it.

   A plan that opens with executable detail can only be reviewed for internal consistency, which is how a wrong design becomes more precise instead of getting fixed. If a row has no rejected alternative it isn't a decision — it's an assumption, and it belongs in the premise list from rule 1.

6. **Absorb mid-stream additions without friction.** When a requirement arrives in turn two, integrate it and re-validate the affected sections only. Don't imply it should have been mentioned sooner, and don't rewrite the whole plan when an edit suffices.

7. **Flag every addition you make that wasn't asked for.** "I'd add a 15-minute window because X" — don't smuggle it into the plan.

8. **When the plan goes to an external reviewer, frame the ask for subtraction.** "Review this plan" can only produce additions — each finding becomes another paragraph, and the plan converges on longer-and-more-defended rather than simpler. Ask instead: what would you delete; what does this assume about the environment that it hasn't verified; describe a simpler design meeting the same goal. Run it **once**, not to consensus — iterating to mutual agreement optimises the document, not the design.

9. **End at your agent's plan-approval step.** If team-facing docs are wanted, ask where they should live (most repos use a `docs/` folder at working or root level; follow whatever convention is already there).

## Local calibration

Everything above is general. The values below are tuned to one person — edit them freely, and let lessons learned about how someone works land *here* rather than rewriting the rules.

- **Structured-question batches:** 3–4 at a time, recommendations first and marked `(Recommended)`. Never one at a time, never more than four.
- **Plan length ceiling:** ~150 lines.
- **Requirement cadence:** expect additions in turns two and three. Absorb, don't reset.
- **Opening move:** they lead with rich framing and directional opinions — don't open with a blank-slate interview.
- **Docs location:** ask before creating; follow the repo's existing convention rather than introducing a new top-level folder.

## What this skill is not

Not a ritual to march through. People open with rich framing and high-level questions naturally — don't manufacture extra steps. Use the rules above to fill the gaps in *your* behaviour.
