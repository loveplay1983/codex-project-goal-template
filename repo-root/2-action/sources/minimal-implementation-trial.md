# minimal-implementation-trial.md

## 1. File role

This file defines the first bounded implementation trial for a Codex project.

It exists to answer one question:

> Can Codex perform one small, safe, reviewable implementation step correctly before the project moves into full milestone execution or `/goal`?

This file should be used only after the read-only trial has already passed.

---

## 2. Why this exists

A project should not jump directly from “Codex understands the repository” to “Codex is now trusted with long-running milestone execution.”

There should be one intermediate step:

- a small implementation task
- with narrow scope
- with explicit allowed files
- with clear forbidden areas
- with a small real verification path
- with an auditable final report

This is the safest bridge between:
- read-only understanding
- durable goal-driven execution

---

## 3. When to use this prompt

Use this prompt when:

- the read-only trial already succeeded
- the instruction stack is stable enough for small implementation work
- the first real milestone should be tested in a bounded way
- the operator wants to verify that Codex can change files without drifting
- the project is about to enter `/goal`, but trust has not yet been established

Do not use this prompt when:

- the project still has conflicting high-level instructions
- the repository understanding trial failed
- the task is already deep in a later milestone and no longer a first implementation test
- the operator wants a full milestone durable run right now

---

## 4. What kind of task this should be

The ideal minimal implementation trial should be:

- small
- low-risk
- easy to verify
- contained to a few files
- clearly earlier than later milestones

Typical good trial tasks include:

- scaffold project structure
- add base config loading
- add a minimal app or service skeleton
- add first import/config sanity path
- add the smallest smoke-checkable entrypoint

Typical bad trial tasks include:

- full schema design plus multiple later layers
- large runtime orchestration
- multi-layer refactors
- assistant integration
- target-machine deployment work
- anything destructive

---

## 5. Required behavior from Codex

During this trial, Codex must:

1. read the authoritative files first
2. stay inside the current milestone boundary
3. keep the file scope narrow
4. avoid entering later milestones
5. explain the plan before changing files
6. run only the minimum checks needed for this bounded task
7. clearly separate:
   - current-machine checks
   - deferred target-machine checks
8. finish with a file-level and verification-level report

If Codex expands into later milestones during this trial, the trial has failed.

---

## 6. Standard minimal implementation trial prompt

Use the following as the default first bounded implementation trial:

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

This is NOT a `/goal` run.

Do only one small bounded implementation step.

Task:
Implement only the smallest safe trial task for the current project, staying within the earliest applicable milestone.

Allowed:
- create or edit only the minimum files required for this trial
- add the smallest config/app/service skeleton needed
- add the smallest sanity-check path needed
- update README.md minimally if a real confirmed command or behavior needs documentation

Forbidden:
- no cross-milestone expansion
- no destructive operations
- no architecture redesign
- no edits outside `4-implementation/`
- no target-machine validation claims
- no plans that depend on Codex operating on the target machine unless explicitly allowed by the project

Before making changes, output exactly these sections:

## 1. Task understanding
## 2. Applicable milestone
## 3. Files and directories to create or modify
## 4. Risks and assumptions
## 5. Planned commands
## 6. Verification plan

Then proceed with implementation.

At the end, report:

1. changed files
2. why each changed file changed
3. commands actually run
4. actual current-machine checks performed
5. what remains deferred
6. whether the project is now ready for the first real `/goal`.

## 7. How to choose the actual first task

The first real implementation trial should usually come from the earliest safe sequence:

1. scaffold structure
2. add base config
3. add base skeleton
4. add first import/config sanity path

Prefer the smallest task that can be verified quickly.

If in doubt, choose the earlier and smaller task.

------

## 8. What a good result looks like

A good result from this trial should show:

- Codex stayed within the intended milestone
- only a small number of files changed
- the changed files are in the correct implementation area
- the change is understandable
- the checks are real
- the final report is concrete
- no later-stage logic was silently added

------

## 9. What a bad result looks like

A bad result includes any of the following:

- Codex jumped into later milestones
- Codex modified unrelated files
- Codex changed architecture without approval
- Codex claimed runtime validation that did not actually happen
- Codex made large edits where a small diff would have been enough
- Codex produced a vague final report
- Codex created more complexity than the task required

------

## 10. Trial success criteria

This minimal implementation trial is successful if all of the following are true:

1. the task stayed inside the intended milestone
2. the file scope stayed narrow
3. the implementation area was respected
4. the checks were real and appropriate
5. the final report was specific
6. the next step is now clearly identifiable
7. the project can safely move to either:
   - one more small manual trial, or
   - the first real `/goal`

------

## 11. Recommended operator response after the trial

If the result is good:

- approve the next milestone step
- decide whether to:
  - run one more small manual trial, or
  - start the first real `/goal`

If the result is partly wrong:

- correct the misunderstanding
- rerun a narrowed version of this trial

If the result is badly wrong:

- stop
- repair the instruction files or file boundaries first
- rerun the read-only trial if needed

------

## 12. Relationship to later `/goal` use

This file should normally be used only once near the beginning of a project, or again after a major instruction reset.

Recommended progression:

1. read-only trial
2. minimal implementation trial
3. review and confirm trust
4. first real milestone `/goal`

This keeps the project stable and reviewable.

------

## 13. Final note

This file exists to answer one question before durable milestone execution begins:

> Can Codex make one small real change correctly, inside scope, with real verification and an honest report?

If the answer is not clearly yes, do not move into `/goal` yet.