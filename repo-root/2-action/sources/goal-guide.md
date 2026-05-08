# goal-guide.md

## 1. File role

This file defines the recommended `/goal` usage discipline for a Codex project.

It is not the project blueprint.
It is not the detailed architecture file.
It is not the collaboration-style file.

Its purpose is to define:

- what kinds of work are suitable for `/goal`
- what kinds of work are not suitable for `/goal`
- how a good goal prompt should be structured
- how to control scope, stop conditions, and verification
- how to keep long-running Codex work bounded and reviewable

This matches official Codex guidance: durable goal-following works best when the objective, constraints, and validation loop are explicit. ([developers.openai.com](https://developers.openai.com/codex/use-cases/follow-goals))

---

## 2. Relation to repository structure

This file belongs in the active authoritative non-code instruction area:

- `2-action/sources/`

Current implementation work should normally treat the following as active guidance:

- root `AGENTS.md`
- `4-implementation/AGENTS.md`
- `2-action/sources/project-overview-and-plan.md`
- `2-action/sources/architecture-design.md`
- `2-action/sources/goal-guide.md`
- `2-action/sources/tutor-prompt.md`

The following directories are historical by default and should not be treated as current implementation truth unless explicitly requested:

- `1-plan/`
- `3-reference/`

---

## 3. What `/goal` is for

`/goal` is for a single durable milestone-level task.

A good `/goal` task should have:

- one clear objective
- one bounded scope
- explicit constraints
- explicit done conditions
- a real verification path
- explicit stop conditions

In short:

> `/goal` is for bounded, reviewable, verifiable long tasks.

Official Codex guidance recommends exactly this style: give Codex a clear objective, constraints, and “done when” criteria so it can iterate without drifting. ([developers.openai.com](https://developers.openai.com/codex/learn/best-practices) ([developers.openai.com](https://developers.openai.com/codex/use-cases/follow-goals)))

---

## 4. What `/goal` is not for

Do **not** use `/goal` for:

- vague exploration
- architecture discovery without prior decisions
- “build the whole project automatically”
- destructive operations
- product decisions that still need human judgment
- tiny one-line or typo-level edits
- broad refactors with unclear acceptance criteria

Bad goals are goals where success cannot be checked cleanly.

---

## 5. Core `/goal` principles

### Principle 1: one goal = one milestone
Do not bundle multiple milestones into one `/goal`.

### Principle 2: boundaries first, execution second
Write scope, constraints, done conditions, and stop conditions before starting.

### Principle 3: manual trial before durable automation
Test the task in a normal thread first before depending on `/goal`.

### Principle 4: verification before “done”
A goal is not complete because Codex says so.
A goal is complete because the required checks passed.

### Principle 5: stop instead of drifting
If a new architecture decision is needed, stop and report.

### Principle 6: keep the report auditable
Every goal should end with a file-level and verification-level report.

These principles are aligned with Codex best practices for long-horizon work and reviewable task execution. ([developers.openai.com](https://developers.openai.com/blog/run-long-horizon-tasks-with-codex) ([developers.openai.com](https://developers.openai.com/codex/learn/best-practices)))

---

## 6. Recommended `/goal` structure

A strong `/goal` prompt should usually contain these sections:

1. Goal
2. Context
3. Scope
4. Constraints
5. Done when
6. Verification
7. Stop conditions
8. Required final report

The smallest safe minimum is:

- Goal
- Context
- Constraints
- Done when

That is also the prompt structure recommended in official Codex best practices. ([developers.openai.com](https://developers.openai.com/codex/learn/best-practices))

---

## 7. Recommended generic `/goal` template

```text
Goal:
Implement [milestone name], and complete only this stage without entering later stages.

Context:
1. Read first:
   - AGENTS.md
   - 4-implementation/AGENTS.md
   - project-overview-and-plan.md
   - architecture-design.md
   - tutor-prompt.md
   - this file
2. The project must follow the current authoritative architecture and implementation rules.
3. If current documents conflict, stop and report the conflict.

Scope:
Only the following files/directories may be changed:
- [fill in]

Do not change:
- [fill in]
- no destructive operations
- no cross-milestone expansion
- no unauthorized dependency expansion

Constraints:
1. Keep architecture stable.
2. Prefer minimal diffs.
3. Preserve layer boundaries.
4. Do not silently redesign the project.
5. Do not assume target-machine behavior is already verified.
6. Stop if a new architecture decision is required.

Done when:
1. [fill in completion standard]
2. [fill in expected output/artifact]
3. [fill in validation standard]

Verification:
- [fill in smoke test / import check / focused test / manual check]
- clearly separate:
  - current-machine checks performed now
  - target-machine checks deferred for later

Stop conditions:
1. Stop if architecture decisions are needed.
2. Stop if destructive operations would be required.
3. Stop if scope would have to expand.
4. Stop if current project documents conflict materially.
5. Stop if the task cannot be completed safely within the current milestone.

Required final report:
1. Which files changed
2. Why each file changed
3. Which commands were actually run
4. Which validations passed now
5. Which validations remain deferred
6. Remaining risks
7. The next smallest reasonable task

## 8. Pre-goal checklist

Before starting `/goal`, check:

1. Is this really one milestone?
2. Is the objective clear?
3. Is the allowed file scope clear?
4. Are the forbidden areas clear?
5. Are the done conditions explicit?
6. Is the verification path explicit?
7. Are stop conditions defined?
8. Does this need a manual trial first?

If two or more of these are unclear, do not start `/goal` yet.

------

## 9. Recommended `/goal` usage rhythm

Recommended sequence:

1. establish repo rules
2. establish project blueprint
3. establish architecture anchor
4. run a read-only trial
5. run a small non-`/goal` implementation trial
6. then start the first real milestone goal
7. review the result
8. only then start the next milestone goal

The general best-practice pattern is: plan first, validate early, then move into longer durable execution. ([developers.openai.com](https://developers.openai.com/blog/run-long-horizon-tasks-with-codex) ([developers.openai.com](https://developers.openai.com/codex/learn/best-practices)))

------

## 10. What good goals look like

### Good example

```text
/goal Implement the core schema/init layer only, keep changes inside 4-implementation/, create the initial tables/models, and stop after a minimal insert/query sanity check passes.
```

Why it is good:

- one milestone
- bounded scope
- clear validation
- easy final report
- easy review

### Another good example

```text
/goal Implement the first local UI detail page only, keep routes thin, do not touch scheduler/runtime code, and stop after the page can render existing item metadata successfully.
```

------

## 11. What bad goals look like

### Bad example

```text
/goal Build the whole project and decide the next steps automatically.
```

Why it is bad:

- multiple milestones
- unclear scope
- no clear validation
- no stop conditions
- high architecture-drift risk

### Another bad example

```text
/goal Refactor everything to make it cleaner.
```

Why it is bad:

- unclear success
- unclear file scope
- hidden expansion risk
- hard to review

------

## 12. Reporting discipline during and after `/goal`

A goal run should always leave behind a usable audit trail.

At minimum, the end report should include:

- changed files
- why each changed file changed
- actual commands run
- actual checks run
- unresolved issues
- remaining risks
- the next smallest reasonable task

If development and deployment happen on different machines, the report must also distinguish between:

- checks completed on the current machine
- checks deferred to the target runtime machine

Do not describe deferred target-machine validation as already passed.

------

## 13. Goal sizing philosophy

Smaller goals are usually safer.

A good rule of thumb:

- if success can be verified in one focused review, the goal is probably sized well
- if the goal touches too many unrelated directories, it is probably too large
- if the final report would be hard to read, the goal is probably too large
- if the task needs multiple human decisions in the middle, it is probably too large

Prefer narrower goals over broader goals.

------

## 14. Relationship between `/goal` and normal threads

Use normal threads for:

- planning
- architectural clarification
- review
- explanation
- tiny edits
- deciding milestone boundaries

Use `/goal` for:

- executing a single already-defined milestone
- durable bounded work
- tasks with clear validation loops

In short:

> plan in normal interaction, execute in bounded goals.

------

## 15. Relationship between `/goal` and collaboration style

`/goal` does not cancel transparency rules.

Even during goal-driven execution, Codex should still:

- read first
- explain what changed
- prefer minimal diffs
- report commands
- report checks
- report risks

The goal mechanism provides durability.
It must not become an excuse for black-box work.

------

## 16. Final note

The point of this file is simple:

> `/goal` should function as a milestone engine, not a project dictator.

A Codex project remains safe and reviewable only when every goal is:

- bounded
- explicit
- verifiable
- stoppable
- reviewable