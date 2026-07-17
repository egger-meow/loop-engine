# CLAUDE.md

This file provides guidance to Claude Code (or any agent reading this
repo's conventions) when working with code in this repository.

## What this is

linkcheck is a CLI that finds broken links (relative paths, heading anchors,
optionally external URLs) across a tree of Markdown files, and can
autofix a narrow, high-confidence subset of breaks. It is a linter first —
catching every real break matters more than fixing some of them
automatically. See `docs/project-charter.md` for the full mission and
guardrails.

## Before you change anything

Read, in this order, if you haven't already this session:

1. [`PRIORITIES.md`](PRIORITIES.md) — what you're authorized to work on next.
2. [`docs/project-charter.md`](docs/project-charter.md) — mission, safety
   principles, and the documentation contract.
3. [`docs/domain-model.md`](docs/domain-model.md) — shared names; don't
   invent new vocabulary for concepts that already have one.
4. [`docs/status.md`](docs/status.md) and
   [`docs/build-status.md`](docs/build-status.md) — what currently exists.

Full procedure: `../../LOOP_ENGINEERING.md`.

## Commands

```bash
npm install
npm run build            # compiles src/ -> dist/
npx linkcheck <dir>      # run the CLI against a doc tree
npx linkcheck <dir> --fix
npx linkcheck <dir> --check-external
npx linkcheck <dir> --format json

npm run lint
npm run typecheck
npm test                 # vitest
npm run verify           # lint + typecheck + test + build, in order — the gate
```

## Architecture

Four-stage pipeline: Discovery → Validation → {Reporting, Autofix}. Only
Validation touches the filesystem or network; Discovery only parses.
Reporting and Autofix both consume Validation's output independently — see
`docs/system-direction.md` for the full boundary rules and
`docs/domain-model.md` for the shared types (`Link`, `Target`, `Broken
Link`, `Autofix Candidate`, `Scan Report`) that cross those boundaries.

## Key references

- [`AGENTS.md`](AGENTS.md) — repo conventions (structure, style, testing,
  commit conventions).
- [`PRIORITIES.md`](PRIORITIES.md) — the active, ordered priority contract.
- [`docs/README.md`](docs/README.md) — index of all canonical docs.
- [`docs/status.md`](docs/status.md) — source of truth for current behavior.
