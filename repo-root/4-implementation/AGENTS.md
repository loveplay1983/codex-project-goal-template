# AGENTS.md

## Scope

This file applies only to work inside `4-implementation/`.

It is subordinate to the repository root `AGENTS.md`.
Follow both files, but when implementation details are needed, this file is more specific and therefore takes precedence for code work inside `4-implementation/`.

---

## Active guidance sources for implementation work

Inside `4-implementation/`, the current authoritative non-code guidance should normally come from:

- root `AGENTS.md`
- `4-implementation/AGENTS.md`
- current authoritative files in `2-action/sources/`

By default, do **not** treat the following directories as active implementation guidance sources:

- `1-plan/`
- `3-reference/`

Those are historical discussion/reference areas and should normally be ignored during implementation work unless the user explicitly requests historical review, legacy design recovery, or archived reference lookup.

---

## Implementation identity

This directory contains the formal implementation of the project.

The production runtime should be defined by the active project blueprint and architecture files, not guessed ad hoc by Codex.

General assumption:

- this directory is where actual code, tests, configs, runtime scripts, and implementation modules belong
- this is not the place for planning notes, prompt drafts, or archived references
- implementation work must preserve project-level architecture and scope constraints

---

## Intended directory structure

Unless the active project defines a different approved structure, prefer something close to:

- `README.md`
- `pyproject.toml` / `package.json`
- `app/` or `src/`
- `tests/`
- `scripts/`
- `config/`
- runtime-related files or folders
- optional `instance/`, `data/`, `logs/`, `systemd/`, or similar directories when the project actually needs them

If the implementation has not yet been scaffolded, create files and directories inside a coherent structure rather than inventing random placement.

If the project blueprint already defines a stronger structure, follow that instead.

---

## Command policy

Do not invent fake commands and present them as already working.

Use this rule:

1. If real commands already exist in this directory, use those.
2. If commands do not exist yet, scaffold the project using the project’s preferred toolchain.
3. After scaffolding, document the actual commands here and in `README.md`.

Preferred command categories to make explicit once they exist:

- environment setup / dependency sync
- run the main app or service
- run tests
- lint
- format
- bootstrap / init / migration / maintenance
- runtime or worker entrypoints, if the project has them

The official Codex guidance is to keep instructions practical and accurate, and update them when the implementation reality changes. ([developers.openai.com](https://developers.openai.com/codex/guides/agents-md) :contentReference[oaicite:1]{index=1})

---

## Read-first and diff-first rules

Before modifying existing code:

1. inspect relevant files first
2. explain current behavior
3. identify the smallest correct change
4. prefer minimal diffs over broad rewrites

Before implementation-oriented work in this directory:

1. read current authoritative guidance first:
   - root `AGENTS.md`
   - this file
   - relevant files in `2-action/sources/`
2. summarize the task and fixed constraints
3. identify relevant files
4. state assumptions, risks, and unknowns
5. if the task is large, propose a milestone-first plan before editing

Only consult `1-plan/` or `3-reference/` when explicitly requested or when historical reasoning or archived references are truly needed.

Do not rewrite large files if a narrow change is sufficient.

---

## Code transparency rules

Before editing:

1. explain the goal
2. explain which files will change
3. explain the main risks
4. explain which commands you plan to run

After editing:

1. provide a diff-style summary
2. explain why each changed file changed
3. report tests, checks, or manual verification
4. report unresolved risks or follow-up work

Do not hide meaningful changes behind vague summaries.

---

## Task discipline

For implementation work:

- do one milestone at a time
- keep scope explicit
- avoid cross-milestone sprawl
- stop when architecture decisions are needed
- stop when requested work conflicts with active project documents
- stop before destructive operations
- do not silently “help” by implementing the next milestone

This matches Codex guidance for bounded goals and durable tasks with clear stop conditions. ([developers.openai.com](https://developers.openai.com/codex/use-cases/follow-goals))

---

## Testing and verification

A task is not done merely because code was written.

### Minimum expectations

Every completed milestone should leave behind:

- runnable code or a valid implementation artifact for the current stage
- a clear verification path
- minimal tests or smoke checks appropriate to the current machine
- an explicit note of what remains

### Preferred verification ladder

1. static sanity check
   - imports resolve
   - config loads
   - module structure is coherent

2. authoring-level smoke check on the current machine
   - app or service skeleton can be constructed where applicable
   - config and paths behave as expected
   - project structure matches the intended layout

3. target-runtime validation on the deployment machine
   - real dependency installation
   - real service startup under the real environment
   - runtime integrations
   - end-to-end behavior where relevant

4. manual validation notes
   - explain what was verified now
   - explain what remains deferred to the target machine

Do not claim target-runtime verification unless it was actually performed on the target machine.

---

## Validation mode rule

If the project uses a split environment, distinguish clearly between:

- development machine = Codex interaction / authoring / generation / local checks
- target machine = deployment / runtime / execution

Therefore:

- do not assume Codex exists on the target machine
- do not generate plans that require Codex to continue operating on the target machine unless the user explicitly says so
- do not describe deferred target-machine checks as passed, completed, verified, or fully working
- always report which checks were performed now and which remain deferred

If the active project provides a stricter environment-split rule, follow that stricter rule.

---

## What "done" means in this directory

For implementation tasks, done means:

- the requested scope is satisfied
- the change is inside `4-implementation/`
- architecture constraints remain intact
- the correct layer handled the task
- relevant checks or smoke tests were run
- remaining risks or follow-up work were reported

If deployment happens on a different machine, “done” must not imply that deployment-machine verification already happened unless it actually did.

---

## First-task rule for an empty implementation directory

If `4-implementation/` is still mostly empty, do not jump directly into complex feature work.

Preferred first sequence:

1. scaffold project structure
2. add the main package/config file
3. add base config and app/service skeleton
4. add first smoke-test or import/config sanity path
5. only then proceed to deeper milestones

This sequencing is also consistent with Codex’s best-practice guidance: start with a clear plan, small verifiable steps, and update instructions as the project becomes real. ([developers.openai.com](https://developers.openai.com/codex/learn/best-practices))

---

## Documentation rule

Whenever a real command, entrypoint, directory, or workflow becomes established here:

- update this file
- update `README.md`
- keep both consistent

This file should describe how the implementation actually works, not how it worked in an earlier draft.

---

## Goal implementation rule

When `/goal` is used for implementation work in this directory:

- keep one goal = one milestone
- keep the allowed file set explicit
- keep forbidden areas explicit
- keep verification explicit
- keep stop conditions explicit
- keep the final report explicit

A good implementation goal should make it obvious:

- what success looks like
- what files may change
- what files may not change
- how the result will be checked
- when Codex should stop and ask for review

---

## Instruction precedence

This file defines implementation-level rules for `4-implementation/`.

If a deeper subdirectory later gets its own `AGENTS.md`, that more local file may define even more specific rules, but it must not violate:

- root `AGENTS.md`
- active project blueprint
- active architecture constraints
- active `/goal` discipline