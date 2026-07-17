# Init Checklist

Order matters here: each step needs the ones before it to be real (not
template placeholders) before it can be filled in honestly. Read
[`LOOP_ENGINEERING.md`](LOOP_ENGINEERING.md) first if you haven't — this
checklist is just the mechanical sequence; that doc is why the sequence is
this way.

Work through this with the human who owns the project — steps 1-4 require
their judgment, not an agent's guess. An agent can draft them, but a human
should confirm before they're treated as authorized.

Keep [`examples/linkcheck/`](examples/linkcheck/) open in another tab as you
go — it's a complete filled-in instance of every file this checklist asks
you to write, so you have a concrete model for each step instead of just the
abstract template.

**Before step 1:** if you copied loop-engine's own `README.md` into your
project, replace it with your project's actual README — loop-engine's
`README.md` describes loop-engine, not your project, and doesn't get
templated like the files below.

- [ ] **1. `docs/project-charter.md`** — Mission, core areas, guardrails.
      This is the highest-authority doc; everything else should trace back
      to it. If you can't fill this in confidently yet, the project isn't
      ready for autonomous looping — spend more time here, not less.
- [ ] **2. `docs/domain-model.md`** — Name the core concepts from the
      charter's "Core Areas." Do this before writing any other doc in
      detail, so later docs use consistent vocabulary from the start instead
      of needing a rename pass.
- [ ] **3. `docs/system-direction.md`** — Target architecture, in enough
      detail to guide real decisions. Can be sparse for a brand-new project
      (there's no "current fit" gap yet); should be substantive for an
      existing codebase being retrofitted with this framework.
- [ ] **4. `docs/status.md`** — For a new project, this starts nearly empty
      plus a defined verification gate command. For an existing codebase,
      this is where you do the honest, detailed accounting of what actually
      works today — the more accurate this is now, the less the agent will
      waste time rediscovering it.
- [ ] **5. `docs/build-status.md`** — The coarse table version of step 4,
      one row per core area from the charter. Seed the Verification Evidence
      log with today's date and whatever's already been verified.
- [ ] **6. `docs/release.md`** — Versioning scheme and checklist. Can be
      minimal for a pre-release project; still worth having so the shape
      exists before it's needed under time pressure.
- [ ] **7. `CLAUDE.md` and `AGENTS.md`** — Fill in commands, structure, and
      conventions. These reference the docs above rather than duplicating
      them — resist the urge to copy content in instead of linking.
- [ ] **8. `PRIORITIES.md`** — Write "What Counts as a Blocker" for this
      project first (this is the step people are tempted to skip or leave
      generic — don't; a vague blocker definition produces a priority queue
      an agent can't reliably reason about). Then seed "Current Priorities"
      with real first items, most urgent first.
- [ ] **9. Delete every remaining `TEMPLATE:` comment.** Run
      `./scripts/check-templates.sh` (or `check-templates.ps1` on Windows)
      instead of grepping by hand — it lists every file and line still
      carrying a `TEMPLATE:` marker and exits nonzero if any remain. A doc
      with a `TEMPLATE:` comment still in it is not yet a source of truth —
      treat it as "not written" until the comment is gone. (`docs/audits/
      TEMPLATE.md` itself is excluded from the scan on purpose — it's meant
      to stay a blank template forever; see `docs/audits/README.md`.)
- [ ] **10. Do one real loop.** Take the first `PRIORITIES.md` item through
      the full procedure in `LOOP_ENGINEERING.md` — implement, verify via
      the gate from `docs/status.md`, update status docs, retire the
      priority item, log the changelog entry. This surfaces any gap in the
      docs above (missing context, an undefined verification gate, an
      ambiguous blocker definition) while it's cheap to fix, before relying
      on the framework for real autonomous work.

Once step 10 is done, an agent working in this repo should be able to start
a fresh session, read `AGENTS.md`/`CLAUDE.md`, and correctly identify what to
work on next without you re-explaining anything from this conversation.
