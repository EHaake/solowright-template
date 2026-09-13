# Getting Started

This file travels with every project created from this template. The
Solowright system itself — the `spec-driven-development` skill:
`SKILL.md`, the reusable templates, the three subagents — lives at
github.com/EHaake/solowright, installed once at
`~/.claude/skills/spec-driven-development/`, not inside this repo. This
file is the quick human reference for actually running a project: how
to set one up, what the files are for, what the day-to-day flow looks
like, and roughly how much of your own time it takes.

## Setting up a new project

### Idea / design phase (chat, before any code exists)

This repo's `CLAUDE.md`, `specs/.../spec.md`, `specs/.../plan.md`, and
`specs/.../tasks.md` already exist, skeletoned with inline guidance
comments — there's nothing to go find or copy. Work through them in
this order, in conversation, before writing any code.

Not every step deserves equal time. The idea itself, the spec, and the
design direction are where iteration genuinely pays off — that's where
most of your engagement should go. The constitution's technical choices
are comparatively fungible; if you don't have a strong preference on
one, say so and expect a quick recommendation rather than a long
exploration — "no preference" should move things along, not open up
more questions.

0. **Idea conversation, before any technical decision.** Audience,
   purpose, what makes this distinctive, the core loop or the point of
   the thing. Settle this before framework/hosting/tooling talk starts —
   technical choices tend to clarify naturally once the idea is clear.
1. **Constitution conversation.** Platform, architecture pattern,
   testing philosophy, dependency policy. Fill in `CLAUDE.md`. Once the
   idea is settled, this should move quickly.
2. **First spec.** Push on ambiguity here — it's nearly free to resolve
   now and expensive later. Fill in `specs/.../spec.md`. Expect this one
   to run bigger than specs that come after it (the skill's `SKILL.md`
   has the full reasoning, under "the first-spec exception," if useful).
3. **Plan.** Translate the spec into real technical design — types,
   data flow, file structure. Fill in `specs/.../plan.md`.
4. **Design brief, if there's a UI.** Fill in `design/brief.md` —
   audience's own visual vocabulary, what to explicitly avoid, a
   signature element if one exists, the skeuomorphism boundary if
   relevant. Hand it to Claude Design (or whatever visual-design process
   is in use). If this project has no UI, delete `design/brief.md`
   entirely rather than leaving it unfilled.
5. **Design exploration.** Iterate on screens with Claude Design until
   they're actually right — this is worth real time, the same way it
   was on the reference project this skill came from. Deliverables:
   screens exported as images, plus a `tokens.md` capturing the actual
   colors/type/spacing Design settled on. Both become implementation
   references, not something handed to Claude Code to import directly.
6. **Tasks.** Ordered, small, independently verifiable. Fill in
   `specs/.../tasks.md`, tiered by risk for review cadence.
7. **`DECISIONS.md` and `ROADMAP.md`** don't need to exist yet — create
   them the first time something needs a home (a business decision that
   isn't technical design, a deferred feature worth remembering).

### Implementation phase (Claude Code)

1. **One-time, if not already done**: confirm
   `~/.claude/agents/skeptical-reviewer.md` is installed — it's
   per-machine, not per-project, so this repo doesn't carry its own
   copy. If it's missing, get it from the skill's own
   `assets/skeptical-reviewer.md`.
2. Open Claude Code in the project's repo. It reads `CLAUDE.md`
   automatically at the start of the session — nothing to hand it
   manually.
3. Hand off with something like the handoff note at the bottom of this
   repo's `tasks.md`: which file to read, where to start, and the
   review cadence for the first phase or two.
4. From there, the collaboration workflow (below) governs what surfaces
   to you and what Claude Code resolves on its own.

## The files, at a glance

| File | Written by | Purpose |
|---|---|---|
| `CLAUDE.md` | You + Claude, in chat | The constitution. Read automatically every Claude Code session. |
| `spec.md` | You + Claude, in chat | What and why. No implementation detail. |
| `plan.md` | You + Claude, in chat; updated during implementation | Technical design — the record of *why*, kept current as decisions get made or reversed. |
| `tasks.md` | Both you/Claude *and* Claude Code, once implementation starts | Ordered execution steps. The one multi-writer file — see the skill's `SKILL.md` for why that needs care. |
| `brief.md` | You + Claude, in chat | Visual/interaction direction, if there's a UI. |
| `tokens.md` | Output of the design process | The actual colors/type/spacing settled on — an implementation reference, not authored ahead of time. |
| `DECISIONS.md` | You + Claude, as needed | Business/product/process context that doesn't fit the structured docs. |
| `ROADMAP.md` | You + Claude, as needed | Backlog of future specs. Deliberately unordered. |

## The implementation flow, briefly

Full version in the skill's `references/collaboration-workflow.md`; the
short form:

- **Routine, well-specified task** → Claude Code just does it.
- **A real decision, not existential** → Plan Mode first, then the
  `skeptical-reviewer` subagent checks the plan, resolved inside the
  same session. You don't see this happen in real time.
- **Infeasible, needs rework, or a genuinely direction-changing
  unknown** → Claude Code stops and asks you directly.

## Your role

Heavy involvement up front — the idea/design phase is where you're
expected to spend real time, iterating in conversation until the spec
and the design are actually right, not just adequate. Once
implementation starts, you don't touch code, and you're not the
mechanism that makes routine decisions happen — Claude Code and the
subagent handle those without you. You're pulled back in specifically
when something in the design turns out not to work as specified, or
when a genuinely new fork in the road appears that didn't exist when the
plan was written. Both are meant to be uncommon, by nature — a
well-iterated spec shouldn't often turn out infeasible, and
direction-changing unknowns are rare almost by definition.

## A worked example

**Setting**: partway through implementing a personal website. `tasks.md`
calls for a projects/portfolio page.

**A routine-but-real decision, resolved without reaching you:**
Claude Code starts the task and self-assesses — there's a real layout
call here (grid vs. list, how much detail per project), so it's not
purely mechanical, but nothing about it is foundational or risky either.
It activates Plan Mode, looks at the site's existing components, and
proposes reusing the homepage's `Card` component in a grid rather than
building something new. Before touching any files, it asks the
subagent to check the plan against `CLAUDE.md` and `plan.md`. The
subagent reads the actual `Card` component, not just a description of
it, and comes back with one real finding: the plan doesn't say what
happens with zero projects, which `spec.md`'s design requirements
explicitly call out as needing real attention. Claude Code revises to
add an empty state, proceeds, and implements it. The only thing that
reaches you is the normal task-completion report — same as any other
task, nothing about this exchange visible in real time.

**Contrast — when it does reach you:** Later on the same page, Claude
Code finds that `brief.md` specified a masonry-style layout, but the
framework in use has no clean way to do true masonry without a
third-party library — and `CLAUDE.md` says no third-party dependencies
without asking first. That's not a judgment call to resolve quietly;
it's a design decision turning out to need rework. Claude Code stops
and asks you directly, rather than silently picking a workaround or
silently adding the dependency.
