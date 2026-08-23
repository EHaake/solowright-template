# Using this template

This repo is a starting scaffold for a new spec-driven-development
project. `How-To-Use.md`, included in this repo, is the full human
guide — setup sequence, what each file is for, the implementation flow,
and a worked example. The methodology's AI-facing side (`SKILL.md`, the
reusable templates this repo's files were instantiated from, the
reviewer subagent) lives separately, installed once at
`~/.claude/skills/spec-driven-development/` — not duplicated here.

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
