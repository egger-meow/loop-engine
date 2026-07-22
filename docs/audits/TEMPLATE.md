<!-- TEMPLATE: Copy this file to `<phase-name>-audit.md` in this folder and
fill it in. Delete this comment block from the copy. Do not fill in this
file itself — it stays a blank template. -->

# `<Phase Name>` — Completion Audit

**Phase authorized:** `<date, and where/how — e.g. link to the ROADMAP.md
phase entry (or its git history, once removed) that authorized it>`
**Audit written:** `<date>`
**Status:** `<Complete | Complete with noted exceptions>`

## Original Acceptance Gates

<!-- List the phase's exit condition exactly as originally written in
ROADMAP.md (pull it from git history if the phase has already been removed).
Don't rephrase gates to make them easier to check off — if a gate was
ambiguous, note that explicitly rather than silently resolving the
ambiguity in the audit. -->

1. `<gate 1, verbatim from ROADMAP.md>`
2. `<gate 2>`

## Evidence, Gate by Gate

<!-- One subsection per gate above. Each must have specific, checkable
evidence — a command + result, a described manual test + outcome, a link to
a passing test file, a dated log entry from build-status.md. -->

### Gate 1: `<restate briefly>`

`<evidence>`

### Gate 2: `<restate briefly>`

`<evidence>`

## Exceptions / Deviations

<!-- Anything that shipped differently than originally scoped, anything
explicitly descoped, anything left for follow-up work (link the follow-up's
new PRIORITIES.md item, Non-Blocking / Later entry, or ROADMAP.md proposal
if one exists). Say
"none" explicitly rather than omitting this section. -->

## Try It Yourself

<!-- Concrete steps for a human to verify this phase matches what they
actually wanted — not more proof it works (that's the Evidence section
above), but an invitation to judge fit. Write real commands and real
things to look at, e.g. "run `npm run dev`, create a Book, drag to
reorder its priority, confirm the Weekly View updates with no duplicate
slot." If this phase has no user-observable surface (an internal
refactor, a data-layer-only change nobody would look at directly), say so
explicitly: "N/A — no user-observable surface this phase." Never omit
this section silently — omission reads as forgetting, not as
"not applicable." -->

## Follow-Up

<!-- Any new PRIORITIES.md items, Non-Blocking / Later items, or ROADMAP.md
phases/proposals that came out of finishing this phase — e.g. a deferred
optional expansion. Link them; do not describe unstarted work here as if it
were part of this audit's evidence.
Also check ../../.loop-engine/FRAMEWORK_FEEDBACK.md: if it gained entries during this phase,
note that here and remind the human it's ready to harvest upstream (see
that file's header for the harvest protocol). -->
