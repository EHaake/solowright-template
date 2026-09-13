# Solowright — Project Template

A starting scaffold for building a software project with
[Solowright](https://github.com/EHaake/solowright): a spec-driven
development (SDD) system for Claude Code, built for a solo builder
rather than a team. You own what the product does — you write the spec
and try the result — and the system plans it, builds it task by task,
reviews its own work at fixed gates, and reports back in plain
language. It is not an enterprise platform and doesn't try to be.

This repo gives a new project its `CLAUDE.md`, a first spec's
`spec.md`/`plan.md`/`tasks.md`, and a design brief, all skeletoned and
ready to fill in.

## Why spec-driven development

Working with AI assistance in a loose, purely conversational way is fine
for something small. On anything with real scope, a few problems show up
reliably: a decision gets made once and then forgotten by the next
session; the same ambiguity gets re-argued because it was never actually
written down; quality varies from task to task depending on how much
attention a given exchange happened to get.

SDD's answer is to make documents, not chat history, the source of
truth. A constitution states the standing rules once. A spec and a plan
get argued over and refined *before* any code exists — when a wrong
assumption is nearly free to fix, rather than expensive to unwind three
implementation phases later. Implementation then proceeds against those
documents, with a real triage for how much scrutiny a given decision
actually deserves: not "loop a human in on everything," and not "never
loop a human in on anything," but a structured process in between that
mostly runs itself.

This isn't a theoretical framework — it was distilled from actually
building a complete, shipped application this way, then refined across
the projects that followed, against what really happened rather than
what seemed like it should work in the abstract. The reasoning behind
each choice, and what was measured, is recorded in the skill repo.

## How the pieces fit together

Three tools, each doing what it's actually good at:

- **Claude (chat)** hosts the project's start. The idea gets worked
  out here, the constitution and the first spec get argued over, and
  the first plan gets drafted — all in conversation, before any code
  exists. Cheap, fast iteration; the point is catching a wrong
  assumption in a five-minute exchange rather than after it's already
  been built. Once code exists, later specs are conversations in Claude
  Code, and plans are drafted there against the real codebase.
- **Claude Design**, if the project has a UI, produces visual references
  — screens, a color and type system, a written brief — not literal
  source code. For a native app or anything that isn't itself a web
  page, treat its output the way a human team would treat a designer's
  mockups: the target to translate toward, not something to import
  wholesale.
- **Claude Code** implements against the approved documents as ground
  truth, running semi-autonomously. The session orchestrates rather
  than types: a planner subagent drafts each plan and task list, an
  implementer subagent builds one task at a time, and a skeptical
  reviewer signs off on plans and checks every phase — each on the
  model tier its job needs. You get a plain-language report after each
  phase and try what was built. Beyond that, a human only gets pulled
  in for two specific situations: something in the design turns out
  infeasible or needs real rework, or a previously-unknown
  consideration surfaces that would materially change the project's
  direction. Everything else proceeds without needing anyone to sign
  off on every step.

## Why this repo and the skill are separate

The actual methodology — the document templates this repo's files were
instantiated from, the detailed principles behind what gets tested and
what verification actually means, the full reasoning behind the
routine/escalate triage above, and the three subagents Claude Code
dispatches — lives in the skill repo,
**[`solowright`](https://github.com/EHaake/solowright)**, installed as
the `spec-driven-development` skill. It's installed once, at the user
level, and applies automatically to every project — this one, and any
other. That separation is deliberate: it
means refining the methodology later means editing one thing, once, not
re-copying updated files into every project that's ever used this
template.

This repo is what you start a project *from*. The skill is what governs
*how* work actually gets done once you have.

## The document flow

`CLAUDE.md` → `spec.md` → `plan.md` → `tasks.md` → implementation, each
gated by review before the next begins. `CLAUDE.md` states the standing
rules (platform, architecture, testing philosophy) once. `spec.md` is
what and why — user-facing behavior and acceptance criteria, no
implementation detail. `plan.md` is the technical design, and the
document that matters most over time, since it's meant to be kept
current as real decisions get made or corrected, not just written once
at the start. `tasks.md` is the ordered, independently-verifiable
execution list Claude Code actually works through. Implementation
doesn't begin until a spec and plan are approved — see `CLAUDE.md`'s own
"Spec-driven workflow" section once it's filled in.

## Before writing anything

1. Confirm the three subagents are installed in `~/.claude/agents/` on
   whatever machine you're using: `skeptical-reviewer.md`,
   `sdd-implementer.md`, and `sdd-planner.md`. They're user-level, not
   per-project — they should **not** be copied into this repo. If any
   is missing, get it from the skill repo's `assets/`.
2. Rename `specs/001-example-feature/` to match this project's actual
   first feature. The `001-` prefix and slug are placeholders — the real
   name is a decision for this specific project, not something a
   template can pre-fill.
3. If this project has no UI, delete `design/brief.md` and the `design/`
   folder — it's only relevant when there's something to design.

## Then

Read `How-To-Use.md` for the full setup sequence, idea phase through
implementation handoff — then work through `CLAUDE.md` and the renamed
`specs/.../spec.md` in conversation before writing any code.

Delete this file once the project has its own real README; keep or
delete `How-To-Use.md` at that point too, whichever you'd rather.
