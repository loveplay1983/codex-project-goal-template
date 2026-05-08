# AGENTS.md

## Repository identity

This repository is a mixed workspace for one Codex-driven project.

It usually contains four kinds of material:

1. historical planning and architectural discussion
2. active execution prompts and Codex/GOAL action materials
3. historical reference notes
4. formal implementation code

Codex must first determine which area is active before making changes.

---

## Standard repository layout

### Historical areas

- `1-plan/`
  Historical planning notes, architectural reasoning, trade-off discussion, and earlier design thinking.

- `3-reference/`
  Historical references, background material, external notes, and archived support documents.

These two directories are historical by default.

Unless the user explicitly asks for historical review, legacy reasoning recovery, or archived reference lookup, do **not** treat them as the current source of truth for implementation work.

### Active operational area

- `2-action/`
  Action-oriented project documents.

- `2-action/sources/`
  Current authoritative non-code instruction area.

This directory should contain the project’s active guidance files, such as:
- project overview
- detailed architecture anchor
- goal guide
- tutor-style collaboration guide
- trial prompts
- milestone runbooks

### Formal implementation area

- `4-implementation/`
  The formal implementation directory.

All actual production code, scripts, configs, tests, runtime files, and implementation modules should live under this directory unless the user explicitly defines a different implementation root.

### Local editor settings

- `.vscode/`
  Local editor settings only.

---

## Historical folder rule

By default, do **not** treat these directories as active implementation guidance:

- `1-plan/`
- `3-reference/`

Use them only when:
- the user explicitly asks for them
- current documents conflict and earlier reasoning must be checked
- design history or archived references are actually needed

For normal work, prefer:
- root `AGENTS.md`
- `4-implementation/AGENTS.md`
- current authoritative files in `2-action/sources/`

---

## Core rule about where work belongs

Do not place production code in:

- `1-plan/`
- `2-action/`
- `2-action/sources/`
- `3-reference/`

Those directories are not implementation targets.

All real implementation work should go under:

- `4-implementation/`

If implementation work is requested and a target file does not yet exist, create it inside `4-implementation/` in the correct subdirectory rather than inside planning or reference folders.

---

## Project identity rule

Every project should define its own production identity in the authoritative non-code files.

Until more specific instructions are provided, assume:

- this repository is using Codex for controlled engineering work
- the production system is whatever is defined in the implementation area and authoritative planning files
- Codex is an implementation accelerator, not the project owner

Do not invent the project architecture from scratch if authoritative files already exist.

---

## Root working rule for Codex

Before implementation-oriented work:

1. Read current authoritative files first.
2. Summarize the task.
3. Identify the active milestone or task scope.
4. Identify relevant files.
5. State assumptions, risks, and unknowns.
6. If the task is large, propose a milestone-first plan before editing.

If files already exist, inspect and explain them before rewriting.

Prefer minimal diffs over large rewrites.

---

## Active instruction layering rule

Codex reads `AGENTS.md` automatically and supports layered instructions, where more local instruction files override broader ones. A practical pattern is:

- global personal rules
- repo root rules
- more specific rules inside subdirectories

Use that same discipline here:
- root `AGENTS.md` = repository-wide rules
- `4-implementation/AGENTS.md` = implementation-level rules
- current files in `2-action/sources/` = project-specific non-code guidance

Keep repository guidance practical and accurate rather than bloated. :contentReference[oaicite:7]{index=7}

---

## GOAL-task rule

Use `/goal` only for a single milestone or other bounded durable task.

A good `/goal` task must have:

- one clear objective
- explicit scope
- explicit constraints
- a clear validation loop
- a stopping condition
- a meaningful final report

Do **not** use `/goal` for:

- vague exploration
- architecture discovery without prior decisions
- destructive operations
- multiple milestones bundled together
- “build the whole project automatically”

When using `/goal`, Codex should know:
- what to achieve
- what not to change
- how to prove progress
- when to stop

This matches official guidance: `/goal` is for durable objectives with clear validation and stop conditions, not open-ended backlogs. :contentReference[oaicite:8]{index=8}

---

## Prompt contract rule

For most medium or large tasks, a good default prompt structure is:

- Goal
- Context
- Constraints
- Done when

This helps Codex stay scoped and easier to review. Official Codex guidance recommends exactly this four-part structure as a strong default. :contentReference[oaicite:9]{index=9}

For long-horizon work, also prefer:
- checkpointed milestones
- acceptance criteria
- runbook-style instructions
- continuous verification
- a short audit/status log

That is the direction official Codex guidance recommends for long tasks. :contentReference[oaicite:10]{index=10}

---

## Planning rule

If the task is complex, ambiguous, or difficult to scope safely:

- plan first
- do not jump directly into code generation

Use planning before coding when:
- architecture could drift
- multiple directories are involved
- the task has hidden assumptions
- the task might need new dependencies
- the task touches deployment or runtime structure

Codex official guidance recommends planning first for difficult tasks and using durable spec files or plan files for longer-running work. :contentReference[oaicite:11]{index=11}

---

## Code transparency rules

Before editing:

1. Explain the goal.
2. Explain which files will change.
3. Explain the main risks.
4. Explain the commands you plan to run.

After editing:

1. Provide a diff-style summary.
2. Explain why each changed file changed.
3. Report tests, checks, or manual verification.
4. Report unresolved risks or follow-up work.

Do not hide large rewrites behind vague phrases like:
- improved logic
- refactored structure
- updated behavior

State concrete file-level changes.

---

## Reviewability rule

Every completed task should leave behind:

- runnable code or a valid planning artifact
- a clear verification path
- minimal tests or smoke checks where appropriate
- an explicit note of what remains
- an operator-readable summary of changes

Codex should not merely generate code; it should help test, check, and review it. Official best practices explicitly recommend pairing changes with verification and review behavior. :contentReference[oaicite:12]{index=12}

---

## Development-machine vs target-machine rule

In projects where Codex runs only on a development machine, always distinguish between:

- development machine = authoring / generation / Codex interaction environment
- target machine = runtime / deployment / execution environment

Therefore:

- do not assume Codex exists on the target machine
- do not describe target-machine work as Codex-driven work
- do not mark deferred target-machine checks as already passed
- keep configs, paths, and scripts as environment-agnostic as possible
- prefer relative paths and config-driven settings over machine-specific assumptions

When reporting verification, always separate:

- checks performed on the development machine
- checks deferred to the target machine

---

## Command policy

Do not invent fake commands and present them as already working.

Use this rule:

1. If real commands already exist, use those.
2. If commands do not exist yet, scaffold the project using the project’s preferred toolchain.
3. Once real commands are established, update the relevant docs so they stay accurate.

Useful repository-inspection commands at the root commonly include:

- `rg --files`
- `rg -n "keyword" 1-plan 2-action 3-reference 4-implementation`
- `git status --short`

---

## What "done" means

For planning and instruction files, done means:

- correct directory placement
- no unnecessary duplication
- terminology consistent with the active project docs
- paths, file names, and links checked
- output aligned with already decided boundaries

For implementation tasks, done means:

- task scope satisfied
- architecture constraints preserved
- changes located in the correct implementation area
- relevant verification completed
- results and remaining risks clearly reported

If deployment happens on a different machine, “done” must not imply that target-machine runtime validation has already happened unless it actually has.

---

## Automation and stability rule

Only turn a workflow into a recurring automation after it is already reliable manually.

Official Codex guidance recommends using automations only after the workflow becomes stable and predictable, and using dedicated worktrees when appropriate. :contentReference[oaicite:13]{index=13}

So the safe order is:

1. define rules
2. run a manual read-first trial
3. run a small bounded implementation trial
4. run one milestone with `/goal`
5. review and stabilize
6. only then consider repeated automation

---

## Instruction precedence

This root `AGENTS.md` defines repository-wide rules.

If `4-implementation/` contains its own `AGENTS.md`, that more local file should define code-specific commands, tests, and conventions for implementation work, while still respecting the root constraints in this file.