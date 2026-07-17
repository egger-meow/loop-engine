# Loop Engineering

This document is the concept guide for this repository. Read it once, fully,
before filling in any template. Everything else in this repo is an
implementation of the ideas below.

## The problem this repo solves

The default way of working with an AI coding agent looks like this: the agent
proposes something, the human says "yes" or "ok", the agent does it, and
repeat. That loop feels productive but most of the "yes/ok" exchanges carry no
information — the human is rubber-stamping because re-explaining the full
context every time is more expensive than just approving. As a project grows,
this gets worse: more surface area, more decisions, more chances the agent
drifts from what was actually intended, and more human attention spent just
keeping the agent pointed the right way.

**Loop engineering** is the practice of front-loading authorization into
written, canonical artifacts so that day-to-day execution doesn't need
per-step human confirmation. The human's judgment gets spent once, in writing,
on direction and priority. The agent's job on every subsequent loop is to
read the current written state, do the next authorized thing, prove it did
that thing correctly, update the written state, and move to the next thing —
without asking permission for work that was already authorized.

This only works if the written state is trustworthy: current, unambiguous,
and structured so an agent can mechanically determine "what's next" and "is
this actually done" without guessing. That's what the file structure in this
repo exists to guarantee.

## The core insight: separate the four kinds of truth

Most projects blur direction, current state, priority, and history together
into one running conversation (chat history, a single sprawling README, or
the agent's memory of "what we talked about"). Loop engineering keeps them in
four separate, single-purpose places:

| Kind of truth | Question it answers | Lives in | Changes how often |
| --- | --- | --- | --- |
| **Direction** | Where is this going, and what must never break? | [`docs/project-charter.md`](docs/project-charter.md), [`docs/domain-model.md`](docs/domain-model.md), [`docs/system-direction.md`](docs/system-direction.md) | Rarely — only when the human decides the goal itself changes |
| **Current state** | What actually exists and works right now? | [`docs/status.md`](docs/status.md), [`docs/build-status.md`](docs/build-status.md) | Every loop that changes behavior |
| **Priority** | What is the agent authorized to work on next? | [`PRIORITIES.md`](PRIORITIES.md) | Every loop — items are removed when done, reordered when danger/priority changes |
| **History** | What happened, and when, with what evidence? | [`CHANGELOG.md`](CHANGELOG.md), `docs/audits/`, git commits | Append-only |

Every one of these has an owner and a shape. None of them is "just notes."
If a fact doesn't fit one of these four, it probably doesn't need to be
written down — or it belongs in a code comment at the point of the actual
constraint.

## The loop

This is the procedure an agent (and a human reviewing the agent) follows on
every iteration of work:

1. **Orient.** Read [`AGENTS.md`](AGENTS.md) / [`CLAUDE.md`](CLAUDE.md) —
   these point at the canonical docs. Read
   [`docs/project-charter.md`](docs/project-charter.md) and
   [`docs/domain-model.md`](docs/domain-model.md) if this is a new session or
   direction may have changed.
2. **Check current truth.** Read [`docs/status.md`](docs/status.md) and
   [`docs/build-status.md`](docs/build-status.md) to know what already exists
   — don't re-derive this from chat memory, and don't trust a stale mental
   model from a previous session.
3. **Take the top item.** Open [`PRIORITIES.md`](PRIORITIES.md). The first
   item under "Current Priorities" is the authorized next unit of work. Do
   not skip down the list to something more interesting — order is a safety
   decision, not a suggestion (see the rules inside that file).
4. **Do the work.**
5. **Prove it, don't just claim it.** Run this project's verification gate
   (see `docs/status.md` or the project's own test/build/lint commands).
   "It should work" is not evidence. A passing gate, a manual walkthrough
   result, or a specific reproduction is evidence.
6. **Update current truth.** Reflect what changed in `docs/status.md` and/or
   `docs/build-status.md`. If this closed out a whole build phase, write an
   audit in `docs/audits/` (see [`docs/audits/README.md`](docs/audits/README.md)).
7. **Retire the priority item.** Remove it from `PRIORITIES.md` per that
   file's own rules — don't leave a trail of struck-through history there;
   history belongs in `CHANGELOG.md` and git, not in the priority queue.
8. **Record history.** Add a `CHANGELOG.md` entry if this is release-visible.
9. **Repeat**, or stop if `PRIORITIES.md` has nothing left that's authorized
   — that's the signal to go back to a human for the next direction-level
   decision, not a signal to invent new work.

## When the agent must stop and ask a human

Loop engineering does not mean the agent never talks to the human — it means
the human's input is reserved for decisions that are actually theirs to make.
Stop and ask when:

- **Nothing in `PRIORITIES.md` covers the situation.** An empty queue, or a
  newly discovered problem that doesn't fit any existing priority, is a
  direction question, not an execution question.
- **A new major build phase needs activating.** Big, optional, or expensive
  bodies of work (see `PRIORITIES.md`'s priority rules) require explicit
  human sign-off before they become "authorized," even if they'd obviously be
  good to build eventually.
- **The action is destructive, irreversible, or touches production/secrets/
  money/access control**, regardless of what's written in `PRIORITIES.md`.
  Written authorization for *what* to build is not authorization to skip
  the judgment calls this framework's own house rules require confirming.
- **Two canonical docs disagree**, or the task requires a decision that no
  canonical doc answers (a genuine product/business call, not an engineering
  one).
- **Priority order itself is ambiguous** — e.g., two blockers seem equally
  dangerous. Reordering `PRIORITIES.md` on a real safety judgment call is a
  human decision; reordering it because item #2 looked more fun is not
  something the agent should ever do.

Everything else — implementing the top priority item, fixing a bug that
blocks it, updating status docs to reflect reality, writing tests — is
already authorized by the fact that it's written down. Do it without asking.

## Why this scales as the project grows

A small project can survive on chat memory and vibes. A large one can't: the
context window can't hold the whole history, the human can't re-explain
intent every session, and "ask me before doing anything" turns into a
bottleneck that makes the agent slower than doing it by hand. Because
direction, state, priority, and history live in specific files with specific
shapes instead of in conversation, a fresh agent session (or a different
agent entirely) can pick up exactly where the last one left off by reading a
bounded set of files — not by reading the whole project history. That's the
actual point of this repo: make "the agent forgot the context" a
non-event, because the context was never only in its head.

## What's in this repo

- [`README.md`](README.md) — what this repo is and how to adopt it into a
  new project.
- [`INIT_CHECKLIST.md`](INIT_CHECKLIST.md) — the order to fill in the
  templates when bootstrapping a new project from this scaffold.
- [`CLAUDE.md`](CLAUDE.md) / [`AGENTS.md`](AGENTS.md) — agent entry points.
  Keep both in sync; different tools read different files.
- [`PRIORITIES.md`](PRIORITIES.md) — the priority queue contract.
- [`CHANGELOG.md`](CHANGELOG.md) — history.
- [`docs/`](docs/README.md) — canonical direction and current-state docs, plus
  `docs/audits/` for phase-completion evidence.
- [`scripts/check-templates.sh`](scripts/check-templates.sh) /
  [`.ps1`](scripts/check-templates.ps1) — finds leftover `TEMPLATE:` markers
  so you can tell what's actually been filled in.
- [`examples/linkcheck/`](examples/linkcheck/) — a complete, fully-filled-in
  instance of every template in this repo, for a small hypothetical CLI
  tool. Read it alongside a template when the abstract version isn't enough.

Every template file below contains `TEMPLATE:` comments marking what to fill
in and what to delete once filled in. Delete the `TEMPLATE:` comments
themselves as you go — a template comment left in a doc that's supposedly
"the source of truth" is a sign the doc hasn't actually been filled in yet.
Run `scripts/check-templates.sh` to find every remaining one at once instead
of hunting by eye.
