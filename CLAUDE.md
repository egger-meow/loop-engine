<!-- TEMPLATE: This is the entry point Claude Code reads automatically in this
repo. Keep it short — it should orient an agent in under a minute and then
point at the canonical docs, not duplicate their content. Mirror any
structural change here into AGENTS.md; the two files should never disagree.
Delete this comment block once filled in. -->

# CLAUDE.md

This file provides guidance to Claude Code (or any agent reading this
repo's conventions) when working with code in this repository.

## What this is

<!-- TEMPLATE: 2-4 sentences. What does this project do, for whom, and what
is it explicitly NOT (e.g. "an operator-assist tool, not an autonomous
bot")? Copy the opening framing from docs/project-charter.md once that's
written — this section should be a compressed pointer to it, not a fork of
it. -->

## Before you change anything

Read, in this order, if you haven't already this session:

1. [`PRIORITIES.md`](PRIORITIES.md) — what you're authorized to work on next.
2. [`docs/project-charter.md`](docs/project-charter.md) — mission, safety
   principles, and the documentation contract.
3. [`docs/domain-model.md`](docs/domain-model.md) — shared names; don't
   invent new vocabulary for concepts that already have one.
4. [`docs/status.md`](docs/status.md) and
   [`docs/build-status.md`](docs/build-status.md) — what currently exists.

Full procedure: [`LOOP_ENGINEERING.md`](LOOP_ENGINEERING.md).

## Commands

<!-- TEMPLATE: fill in the actual install/run/test/lint/build commands for
this project, e.g.:

```bash
<install command>
<run command>
<test command>
<lint/typecheck command>
```

If there's a single bundled "verification gate" command (recommended — see
docs/status.md), call it out explicitly here as the thing to run before
calling any change done. -->

## Architecture

<!-- TEMPLATE: Short orientation to the codebase layout and the handful of
non-obvious invariants a change is likely to break — the things a new
contributor (human or agent) would get wrong without being told. Link to
docs/system-direction.md and docs/domain-model.md for anything longer than a
paragraph; don't duplicate them here. Delete this section if
docs/system-direction.md already covers it well enough that a pointer is
sufficient. -->

## Key references

- [`AGENTS.md`](AGENTS.md) — repo conventions (structure, style, testing,
  commit conventions).
- [`PRIORITIES.md`](PRIORITIES.md) — the active, ordered priority contract.
  Treat it as authorization, not a backlog to reorder at will.
- [`docs/README.md`](docs/README.md) — index of all canonical docs.
- [`docs/status.md`](docs/status.md) — source of truth for current behavior.
