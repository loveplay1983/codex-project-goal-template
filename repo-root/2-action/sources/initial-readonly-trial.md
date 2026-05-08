# initial-readonly-trial.md

## 1. File role

This file defines the first safe read-only trial prompt for a Codex project.

Its job is to verify that Codex can:

- read the current authoritative files
- identify the active project rules
- distinguish active guidance from historical folders
- summarize the project correctly
- identify the current milestone and risks
- avoid changing files too early

This file should be used before:

- the first real implementation prompt
- the first `/goal`
- any milestone-level autonomous run
- any trial where repo understanding still needs to be checked

---

## 2. Why this exists

A Codex project should not begin with direct code generation.

Before editing, Codex should first prove that it can:

- read the right files
- understand the repo structure
- identify the real constraints
- avoid using archived material as current truth
- propose a bounded next step

This is the safest first check for a new repository or a newly prepared instruction stack.

---

## 3. When to use this prompt

Use this prompt when:

- the project instruction stack has just been created
- the repo structure has just been reorganized
- a new Codex environment is being tested
- a new project is starting
- the operator wants to verify Codex understanding before implementation
- the authoritative files were edited and need a quick consistency check

Do not use this prompt when:

- you already confirmed repo understanding and are ready for a minimal implementation trial
- the task is already deep inside a later milestone
- the current need is code review or debugging rather than project onboarding

---

## 4. Expected behavior from Codex

Codex should:

1. read the listed authoritative files first
2. not modify any file
3. not create any file
4. not infer architecture from archived folders by default
5. summarize the project using the active files
6. identify the current milestone or safest next milestone
7. state risks, unknowns, and what it will not do yet

If Codex starts editing files during this trial, the trial has failed.

---

## 5. Standard read-only trial prompt

Use the following prompt as the default first trial:

```text
Read the current authoritative project instructions first.

Read these files before doing anything else:

1. AGENTS.md
2. 4-implementation/AGENTS.md
3. 2-action/sources/project-overview-and-plan.md
4. 2-action/sources/architecture-design.md
5. 2-action/sources/goal-guide.md
6. 2-action/sources/tutor-prompt.md

Important repository rules:
- Treat `2-action/sources/` as the current authoritative non-code instruction area.
- Treat `4-implementation/` as the formal implementation area.
- Treat `1-plan/` and `3-reference/` as historical/archive areas that should be ignored by default unless explicitly needed.

This is a read-only trial.
Do not modify, create, rename, move, or delete any files.

Your output must contain exactly these sections:

## 1. Project understanding
## 2. Active instruction sources
## 3. Historical areas to ignore by default
## 4. Applicable current milestone
## 5. Fixed constraints
## 6. Relevant files or directories for the next step
## 7. Risks and unknowns
## 8. Safest next bounded task

Important:
- Do not generate code.
- Do not propose implementation beyond the next bounded task.
- Do not use `/goal`.
- Do not assume the target runtime machine is the same as the current Codex machine unless the files explicitly say so.

## 6. What a good output should contain

A good read-only trial output should clearly show:

- the project’s identity
- the current active source-of-truth files
- the difference between active and historical folders
- the current safest milestone
- the most relevant implementation area
- major constraints that cannot be violated
- the next smallest reasonable task

A good output should not:

- jump into code
- suggest large refactors
- pull archived planning notes into current truth without reason
- bundle multiple milestones together
- pretend that target-machine validation already happened

------

## 7. How to judge whether Codex passed the trial

The trial is successful if Codex does all of the following:

1. correctly identifies the active authoritative files
2. correctly identifies historical folders as non-default inputs
3. correctly places implementation work under `4-implementation/`
4. correctly summarizes the project at a high level
5. identifies a bounded next task
6. does not edit files
7. does not widen scope prematurely

The trial is unsuccessful if Codex does any of the following:

- starts generating code
- starts rewriting files
- treats `1-plan/` or `3-reference/` as active truth without justification
- proposes a giant all-at-once implementation jump
- ignores environment-split or validation-split rules
- cannot identify the next bounded milestone

------

## 8. Recommended operator response after the trial

If the output is good:

- approve the next bounded task
- move to `minimal-implementation-trial.md`

If the output is partly wrong:

- correct the misunderstanding
- rerun this read-only prompt once

If the output is badly wrong:

- do not proceed to implementation
- fix the authoritative files first
- rerun this trial afterward

------

## 9. Relationship to later steps

This file is step zero of the safe Codex workflow.

Recommended sequence:

1. prepare instruction stack
2. run `initial-readonly-trial.md`
3. run `minimal-implementation-trial.md`
4. review results
5. only then start the first real `/goal`

This keeps the project auditable and reduces early drift.

------

## 10. Final note

This file exists to answer one question before any real implementation begins:

> Does Codex actually understand the repository, the active rules, and the current boundary of work?

If the answer is not clearly yes, do not start real implementation yet.