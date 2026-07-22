# Examples

[English](README.md) · [繁體中文](zh-TW/README.md)

[`linkcheck/`](linkcheck/) is a complete, fully-filled-in instance of the
loop-engine scaffold for a small hypothetical CLI tool. Every `TEMPLATE:`
comment from the root scaffold has been replaced with real content — no
placeholders remain (`../scripts/check-templates.sh examples/linkcheck`
reports clean).

It exists to answer "what does a *filled-in* version of this actually look
like," which is hard to picture from templates alone. Read it alongside
[`../INIT_CHECKLIST.md`](../INIT_CHECKLIST.md) (or its Chinese translation,
[`../zh-TW/INIT_CHECKLIST.md`](../zh-TW/INIT_CHECKLIST.md)): each file in
`linkcheck/` corresponds 1:1 to a step in that checklist.

linkcheck itself isn't a real, working tool — it's a plausible small CLI
(scans a docs tree for broken markdown links, with an opt-in autofix mode)
invented specifically to have interesting-enough guardrails, a real blocker
definition, and one completed build phase worth auditing, without needing a
proprietary or unrelated real codebase as the example.

One file is shown in a state worth noticing: `linkcheck/ROADMAP.md` shows
all three sections populated at once (an active phase, an authorized next
phase, and unauthorized proposals), which is what a mid-flight project
looks like.

Do not copy `linkcheck/`'s *content* into your project — copy its *shape*.
Your charter, domain model, and priorities should reflect your actual
project, not a docs-link-checker's.
