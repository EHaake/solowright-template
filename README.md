# Spec-Driven Development — Project Template

A starting scaffold for building a software project with Claude, using
spec-driven development (SDD): a `CLAUDE.md`, a first spec's
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
building a complete, shipped application this way, refined against what
really happened during that build rather than what seemed like it should
work in the abstract.

## How the pieces fit together

Three tools, each doing what it's actually good at:

- **Claude (chat)** is the planning partner. The idea gets worked out
  here, the spec gets argued over, the technical plan gets drafted — all
  in conversation, before any code exists. Cheap, fast iteration; the
  point is catching a wrong assumption in a five-minute exchange rather
  than after it's already been built.
- **Claude Design**, if the project has a UI, produces visual references
  — screens, a color and type system, a written brief — not literal
  source code. For a native app or anything that isn't itself a web
  page, treat its output the way a human team would treat a designer's
  mockups: the target to translate toward, not something to import
  wholesale.
- **Claude Code** implements against the approved documents as ground
  truth, running semi-autonomously. Most decisions resolve inside
  Claude Code itself — via a structured self-review process, including a
  second opinion from a dedicated reviewer subagent before anything
  genuinely uncertain — and a human only gets pulled in for two specific
  situations: something in the design turns out infeasible or needs real
  rework, or a previously-unknown consideration surfaces that would
  materially change the project's direction. Everything else proceeds
  without needing anyone to sign off on every step.

## Why this repo and the skill are separate

The actual methodology — the document templates this repo's files were
instantiated from, the detailed principles behind what gets tested and
what verification actually means, the full reasoning behind the
routine/escalate triage above, and the reviewer subagent Claude Code
consults — lives in a companion repo,
**[`SDD-Skill`](https://github.com/EHaake/SDD-Skill)**. It's
installed once, at the user level, and applies automatically to every
project — this one, and any other. That separation is deliberate: it
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

1. Confirm `~/.claude/agents/skeptical-reviewer.md` is installed on
   whatever machine you're using. It's user-level, not per-project — it
   should **not** be copied into this repo. If it's missing, get it from
   the skill's own `assets/skeptical-reviewer.md`.
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
