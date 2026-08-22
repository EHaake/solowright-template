# Using this template

This repo is a starting scaffold for a new spec-driven-development
project — not the methodology itself. For the full reasoning behind why
it's shaped this way, see the `spec-driven-development` skill package
(kept separately, not duplicated into every project created from this).

## Before writing anything

1. Confirm `~/.claude/agents/skeptical-reviewer.md` is installed on
   whatever machine you're using. It's user-level, not per-project — it
   should **not** be copied into this repo. If it's missing, get it from
   the skill package's `assets/skeptical-reviewer.md`.
2. Rename `specs/001-example-feature/` to match this project's actual
   first feature. The `001-` prefix and slug are placeholders — the real
   name is a decision for this specific project, not something a
   template can pre-fill.
3. If this project has no UI, delete `design/brief.md` and the `design/`
   folder — it's only relevant when there's something to design.

## Then

Work through `CLAUDE.md` and the renamed `specs/.../spec.md` in
conversation before writing any code — see the skill package's
`README.md` for the full setup sequence, idea phase through
implementation handoff.

Delete this file once the project has its own real README.
