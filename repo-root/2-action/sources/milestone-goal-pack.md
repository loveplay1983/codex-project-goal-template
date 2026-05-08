# milestone-goal-pack.md

## 1. File role

This file contains reusable milestone `/goal` prompts for a Codex project.

Its job is not to define the architecture from scratch.
Its job is not to replace the project blueprint.
Its job is not to replace the goal discipline file.

Its job is to provide a ready-to-use pack of milestone prompts that can be copied into Codex one by one.

This file should only be used after:

1. the instruction stack is stable
2. the read-only trial has passed
3. the minimal implementation trial has passed
4. the operator is ready to move milestone-by-milestone

---

## 2. How to use this file

Use only one milestone goal at a time.

Recommended sequence:

1. choose the next milestone
2. copy the matching goal prompt
3. fill in project-specific file paths if needed
4. send it to Codex
5. review the output
6. do not start the next milestone until the current one is reviewed

Do not paste multiple milestone goals at once.

---

## 3. Global rules for every milestone goal

Every goal in this file assumes:

- current authoritative files must be read first
- implementation belongs in `4-implementation/`
- `1-plan/` and `3-reference/` are historical by default
- scope must stay inside one milestone
- verification must be explicit
- target-machine validation must not be faked
- final report must be concrete

---

## 4. Milestone 1 — Project skeleton and base configuration

/goal Implement Milestone 1 only: create the project skeleton, base configuration layer, and minimal app/service scaffold inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- create or adjust only the smallest files needed for:
  - project structure
  - base config loading
  - minimal app/service skeleton
  - first import/config sanity path
  - minimal README updates if real commands become confirmed

Do not:
- implement the schema/data layer
- implement discovery/input logic
- implement processing/fetch logic
- implement transformation/extract logic
- implement analysis/AI logic
- implement runtime orchestration
- implement assistant/control integration
- redesign architecture

Constraints:
- keep changes minimal
- preserve clear layer boundaries
- keep the project easy to review
- do not claim target-runtime validation
- do not assume Codex exists on the target machine unless explicitly stated elsewhere

Done when:
- the project structure exists
- base config can load
- the minimal app/service skeleton exists
- a first authoring-level sanity check passes
- the final report is complete

Verification:
- run import/config sanity
- run the smallest app/service construction check if applicable
- separate current-machine checks from deferred target-machine checks

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether Milestone 2 is now ready

##  5. Milestone 2 — Core schema / state / initialization layer

/goal Implement Milestone 2 only: build the core schema/state/init layer inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only the minimum files required for:
  - initial schema/data structures
  - initialization logic
  - core models/tables/state objects
  - a minimal sanity check for create/init + insert/query or equivalent

Do not:
- implement discovery/input logic
- implement fetch/processing logic
- implement extract/transformation logic
- implement UI pages beyond the minimum already present
- implement runtime orchestration
- implement assistant/control integration

Constraints:
- keep the state layer compact and explicit
- preserve separation between metadata/state and primary artifacts
- do not silently redesign the project
- prefer minimal diffs and focused checks

Done when:
- initialization works
- core structures exist
- a simple insert/query or equivalent sanity path passes
- the final report is complete

Verification:
- current-machine initialization check
- current-machine focused sanity test
- clearly separate deferred target-machine work

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether Milestone 3 is now ready

## 6. Milestone 3 — First discovery / intake layer

/goal Implement Milestone 3 only: create the first discovery or intake layer inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only:
  - source/input loading
  - candidate item discovery/intake
  - initial deduplication or intake protection
  - minimal linkage into the current state layer
  - minimal focused validation

Do not:
- implement processing/fetch
- implement transformation/extract
- implement derived-output analysis
- implement runtime orchestration beyond what is strictly needed to test this layer

Constraints:
- discovery/intake is not processing
- keep candidate outputs lightweight
- keep failures visible
- do not expand into later milestones

Done when:
- candidate work items can be discovered or loaded
- duplicates do not repeatedly enter the same path
- the layer can be validated in a small focused way
- the final report is complete

Verification:
- run a minimal intake/discovery sanity path
- show how duplicates are handled
- report current-machine checks separately from deferred runtime validation

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether Milestone 4 is now ready

## 7. Milestone 4 — Processing / fetch layer
/goal Implement Milestone 4 only: build the primary processing/fetch layer inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only:
  - primary processing/fetch path
  - status recording
  - raw artifact persistence where relevant
  - minimal escalation logic if the project uses one
  - focused validation for this stage

Do not:
- implement transformation/extract
- implement analysis logic
- implement broad UI work
- implement runtime scheduling

Constraints:
- preserve a raw evidence/input layer
- make failures explicit
- do not hide retry logic everywhere
- do not expand into later milestones

Done when:
- the first real raw data path works
- raw output is stored correctly
- failures are visible
- the final report is complete

Verification:
- current-machine focused fetch/process validation
- artifact existence/path check where relevant
- honest separation from deferred target-runtime checks

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether Milestone 5 is now ready


## 8. Milestone 5 — Transformation / extract layer
/goal Implement Milestone 5 only: build the transformation/extract layer inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only:
  - transformation/extraction logic
  - normalized output handling
  - fallback path if needed
  - minimal linkage to the existing state layer
  - focused validation for this stage

Do not:
- implement analysis/derived outputs
- implement runtime orchestration
- implement broad UI work
- redesign prior layers

Constraints:
- raw is not cleaned/normalized
- preserve provenance
- make transformation failures explicit
- keep changes milestone-bounded

Done when:
- normalized output is produced from raw input
- outputs are stored in the correct layer
- failures are visible
- the final report is complete

Verification:
- run the smallest real transform/extract check
- confirm output artifacts or normalized state
- separate current-machine checks from deferred runtime validation

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether Milestone 6 is now ready

## 9. Milestone 6 — Storage and versioning linkage

/goal Implement Milestone 6 only: establish stable storage/versioning linkage inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only:
  - stable artifact path conventions
  - version-aware output linkage where relevant
  - metadata/state linkage between canonical items and derived versions
  - focused validation for consistency

Do not:
- implement broad UI work
- implement runtime orchestration
- implement optional assistant/control logic

Constraints:
- provenance must remain traceable
- state must not replace artifact storage
- do not overwrite historical outputs by default if the project expects versioning
- keep the change scoped to storage/version linkage

Done when:
- multiple outputs per item can be represented where relevant
- paths and metadata remain consistent
- provenance is traceable
- the final report is complete

Verification:
- validate path consistency
- validate version/state linkage
- report current-machine checks honestly

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether Milestone 7 is now ready

## 10. Milestone 7 — UI / inspection layer
/goal Implement Milestone 7 only: build the first UI/API/operator inspection layer inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only:
  - first list/detail inspection surfaces
  - narrow safe operator actions
  - route/handler/view logic needed for this stage
  - focused validation for this stage

Do not:
- turn the UI into the scheduler
- bury heavy processing in handlers
- implement runtime orchestration
- implement optional assistant/control integration

Constraints:
- UI is not scheduler
- routes/handlers should stay thin
- important state and artifacts must be visible
- keep the work milestone-bounded

Done when:
- a local operator can inspect key items/state
- narrow safe actions can be triggered where applicable
- the UI/API layer can be validated in a focused way
- the final report is complete

Verification:
- local rendering or endpoint sanity
- focused interaction check
- clear separation from deferred target-runtime checks

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether Milestone 8 is now ready

## 11. Milestone 8 — Analysis / derived outputs
/goal Implement Milestone 8 only: add the first analysis or derived-output layer inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only:
  - first derived-output or analysis integration
  - storage of derived artifacts
  - linkage from source item to derived output
  - focused validation for this stage

Do not:
- implement runtime orchestration
- implement optional assistant/control integration
- redesign previous layers

Constraints:
- derived outputs should remain inspectable
- keep provenance visible
- do not hide model/template/config choices if AI is used
- keep the scope limited to the first derived-output path

Done when:
- at least one existing item can produce one derived output
- outputs are stored correctly
- metadata/state links point to the right place
- the final report is complete

Verification:
- run one real derived-output path
- validate artifact existence and linkage
- clearly separate deferred runtime-only validations

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether Milestone 9 is now ready

## 12. Milestone 9 — Runtime orchestration

/goal Implement Milestone 9 only: add runtime orchestration inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only:
  - scheduler/background orchestration
  - worker/executor logic
  - persistence/restart wrappers if the project requires them
  - focused validation for this stage

Do not:
- redesign prior layers
- hide orchestration logic inside UI handlers
- implement optional assistant/control integration

Constraints:
- UI is not scheduler
- scheduler and worker responsibilities should remain explicit
- failures must be observable
- milestone boundaries must be preserved

Done when:
- work can be dispatched automatically
- worker execution is explicit
- basic orchestration can be validated
- the final report is complete

Verification:
- focused current-machine orchestration checks where safe
- honest distinction between authoring-level validation and deployment-only validation

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether Milestone 10 is now ready

## 13. Milestone 10 — Testing, logging, and stabilization

/goal Implement Milestone 10 only: add testing, logging, and stabilization improvements inside `4-implementation/`, without entering later milestones.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only:
  - smoke tests
  - clearer logs
  - failure visibility
  - bounded retry behavior if relevant
  - validation documentation updates

Do not:
- redesign the architecture
- implement optional assistant/control integration
- silently revisit unrelated milestones

Constraints:
- tests should reflect real project behavior
- logs should help debugging
- failure states should remain visible
- keep changes focused on stability and validation

Done when:
- the core pipeline has a repeatable validation path
- logs are usable
- failures are more diagnosable
- the final report is complete

Verification:
- run the most relevant current-machine checks
- report what still requires target-runtime validation
- keep the report honest and scoped

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether the project is ready for optional assistant/control integration or deployment preparation

## 14. Optional Milestone 11 — Assistant / control integration

/goal Implement Optional Milestone 11 only: add assistant/control integration inside `4-implementation/` after the main runtime is stable, without redesigning the core runtime.

Before doing anything:
- read AGENTS.md
- read 4-implementation/AGENTS.md
- read 2-action/sources/project-overview-and-plan.md
- read 2-action/sources/architecture-design.md
- read 2-action/sources/goal-guide.md
- read 2-action/sources/tutor-prompt.md

Hard scope:
- work only inside `4-implementation/`
- implement only:
  - narrow assistant/control triggers
  - state inspection entrypoints
  - safe operator-facing assistant actions

Do not:
- replace the production runtime with the assistant layer
- move scheduler responsibilities into the assistant layer
- redesign earlier milestones

Constraints:
- assistant/control remains optional
- assistant/control is not the main runtime
- only narrow safe operations are allowed
- keep the core runtime intact

Done when:
- the assistant/control layer can trigger or inspect safe narrow operations
- the core runtime boundaries remain intact
- the final report is complete

Verification:
- current-machine focused checks
- explicit note of anything still deferred to deployment/runtime environments

Required final report:
1. changed files
2. why each file changed
3. commands actually run
4. validations passed now
5. validations deferred
6. remaining risks
7. whether the assistant/control integration remains safely bounded

## 15. Operator rule for using this pack

When using this pack:

- copy only one milestone goal at a time
- do not merge goals
- do not skip review between milestones
- do not start the next goal until the current goal’s final report is reviewed
- if a milestone was only partly completed, either:
  - rerun a narrowed version of the same milestone, or
  - repair the blocking issue in a smaller manual prompt first

------

## 16. Final note

This file exists so that a Codex project can move from:

- stable instructions
- to stable trials
- to stable milestone execution

without turning `/goal` into a vague all-purpose automation bucket.

The intended meaning is simple:

> one milestone, one goal, one review, then next milestone