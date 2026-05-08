# project-overview-and-plan.md

## 1. File role

This file is the high-level project blueprint.

It is not the repository-wide behavior file.
It is not the detailed architecture deep-dive.
It is not the `/goal` usage manual.

This file exists to give Codex and the human operator a stable, concise answer to these questions:

- What is this project trying to build?
- What is explicitly in scope and out of scope?
- What architecture has already been fixed?
- In what order should implementation proceed?
- What counts as completion for each stage?

Recommended instruction layering for a Codex project:

- root `AGENTS.md` → repository-wide rules
- `4-implementation/AGENTS.md` → implementation-level rules
- this file → project blueprint and milestone order
- detailed architecture file → deeper structural anchor
- goal guide → `/goal` discipline
- tutor prompt → explain-first collaboration style

---

## 2. Project overview

This project builds a Codex-assisted software system through a staged, reviewable workflow.

The project may be a web application, automation system, data workflow, local tool, backend service, UI project, or other engineering system, but regardless of domain it should be developed under the same core principles:

- clear scope
- stable architecture boundaries
- milestone-by-milestone delivery
- human reviewability
- explicit verification
- no black-box autonomous drift

This project is not “let the agent build everything however it wants.”
This project is “use Codex as a controlled engineering accelerator.”

---

## 3. Operational repository boundary

Within this repository, the directories that should normally matter for active project work are:

- `2-action/`
- `4-implementation/`

More specifically:

- `2-action/sources/` is the current authoritative non-code instruction area
- `4-implementation/` is the formal implementation area

The following directories are historical by default and should not be treated as active sources of truth unless explicitly requested:

- `1-plan/`
- `3-reference/`

Implementation and project decisions should be based on current authoritative documents, not on archived discussion or background material unless historical review is explicitly needed.

---

## 4. Current development mode

A Codex project may run in one of two modes:

### Mode A: same-machine mode
- development and runtime happen on the same machine

### Mode B: split-machine mode
- development happens on one machine
- deployment/runtime happens on a different target machine

When split-machine mode is active, current implementation work should prioritize:

- target-ready project structure
- environment-agnostic configuration
- deployable code and templates
- honest separation between current-machine checks and target-machine checks
- no assumptions that Codex will exist on the target machine

If the project-specific documents define a stricter environment split, follow the stricter rule.

---

## 5. Primary goals

Every Codex project should aim to achieve the following high-level goals:

1. Build a real working system, not just produce draft code.
2. Keep the implementation understandable and auditable.
3. Keep project structure maintainable.
4. Keep rules, docs, and commands consistent with reality.
5. Deliver milestone by milestone rather than through uncontrolled one-shot generation.
6. Preserve a human-governed workflow where Codex accelerates execution but does not replace project ownership.

---

## 6. Non-goals

The following are explicitly out of scope unless later approved:

- letting Codex decide the entire project architecture on its own
- letting `/goal` silently span multiple milestones
- large destructive changes without explicit approval
- uncontrolled refactors across unrelated modules
- fake completion without verification
- using historical notes as active truth by default
- treating “code exists” as equivalent to “the milestone is complete”

---

## 7. Fixed architecture decisions

This file does not define domain-specific architecture in full detail.
That belongs in the detailed architecture file.

But every project using this pattern should fix the following categories before deep implementation begins:

### 7.1 System boundary
- what the system is
- what it is not

### 7.2 Main layers
Define the major layers explicitly.
Typical layers may include:
- input/discovery
- processing/fetch
- transformation/extract
- storage/index
- UI/API
- runtime/scheduler/worker
- analysis/inference
- external integrations

### 7.3 Responsibility separation
Every project must keep layer boundaries explicit.
For example:
- input is not processing
- processing is not transformation
- UI is not scheduler
- metadata is not full-content storage
- assistant/control layer is not necessarily the production runtime

### 7.4 Validation boundary
Define what can be verified on the development machine and what must wait for target runtime.

---

## 8. Design principles

This project should follow these principles.

### 8.1 Reviewability
Every implementation step should remain understandable, inspectable, and reversible.

### 8.2 Incremental delivery
Build a minimal working version first.
Do not front-load advanced features before the basic pipeline works.

### 8.3 Layer separation
Keep major responsibilities separated.
Avoid hidden coupling and misplaced logic.

### 8.4 Practicality over hype
Prefer boring, stable, maintainable choices over fashionable ones.

### 8.5 Human-governed automation
Use Codex and `/goal` as controlled engineering tools, not as project dictators.

### 8.6 Verification-first completion
A stage is complete only when the defined verification path has actually passed.

---

## 9. Key implementation boundaries

The following boundaries must be respected during development:

- one milestone at a time
- one active scope at a time
- no silent architecture drift
- no hidden expansion into later milestones
- no fake validation
- no confusing planning docs with implementation code
- no default reliance on historical folders

---

## 10. Data / state / artifact philosophy

Every project should define a clear philosophy for where the real system state lives.

Typical pattern:

- filesystem stores implementation files, runtime artifacts, configs, or generated outputs
- structured data stores hold metadata, indexes, relationships, statuses, or pointers
- UI surfaces display and operate on those artifacts
- logs and runtime traces remain observable

The detailed project architecture file should define the exact state model for the project domain.

---

## 11. Milestone plan

Development should proceed milestone by milestone.

Below is the recommended generic sequence for a Codex-driven project.

### M1. Project skeleton and configuration
Deliver:
- project structure
- environment setup
- base config loading
- basic app/service skeleton
- directory initialization

Done when:
- the project layout exists
- the config layer loads correctly
- the base skeleton is ready for later expansion
- authoring-level checks pass on the current machine where possible

### M2. Core data/schema/init layer
Deliver:
- initial schema or data model
- initialization logic
- core structures/tables/models
- simple smoke validation

Done when:
- initialization works
- core structures exist
- a simple insert/query or equivalent sanity path works

### M3. First real input/discovery layer
Deliver:
- source/input loading
- first discovery/intake path
- basic deduplication or intake protection

Done when:
- candidate work items can be discovered/loaded/recorded
- duplicates do not repeatedly enter the same path
- source-level runs can be tracked where relevant

### M4. Processing/fetch layer
Deliver:
- primary processing/fetch path
- clear status recording
- raw artifact persistence where relevant
- escalation rule if the project needs one

Done when:
- the first real data path can run
- failures are visible and logged
- outputs are stored in the correct layer

### M5. Transformation/extract layer
Deliver:
- transformation/extraction logic
- normalized outputs
- fallback path if needed

Done when:
- normalized output is produced
- raw and transformed layers stay separated where applicable
- transformation failures are explicit

### M6. Storage/versioning linkage
Deliver:
- stable path conventions
- versioned derived outputs where relevant
- metadata linkage between canonical items and versions

Done when:
- the project can represent multiple outputs per item
- provenance remains traceable
- state and file paths remain consistent

### M7. UI / inspection layer
Deliver:
- first local UI, API, or inspection interface
- list/detail views or equivalent
- narrow operator actions

Done when:
- a local user/operator can inspect the system state
- important artifacts and metadata are visible
- narrow safe actions can be triggered

### M8. Analysis / derived output layer
Deliver:
- first inference, analysis, or derived-output integration
- prompt/config/template setup where relevant
- artifact writing

Done when:
- an existing item can produce at least one derived output
- outputs are stored and linked correctly

### M9. Runtime orchestration
Deliver:
- scheduler / worker / background task model
- persistence/restart approach
- service definitions or runtime wrappers

Done when:
- work can be dispatched automatically
- runtime behavior is explicit
- restart and logging behavior are documented

### M10. Testing, logging, and stabilization
Deliver:
- smoke tests
- clearer logs
- bounded retry behavior
- documented validation steps
- failure visibility

Done when:
- the core pipeline has a repeatable validation path
- logs are usable for debugging
- basic recovery procedures are documented

### M11. Optional assistant/control integration
Deliver only after the main runtime is stable.

Possible responsibilities:
- trigger narrow operations
- inspect state
- query stored knowledge
- initiate safe reprocessing

Done when:
- the assistant layer remains outside the core runtime loop
- no architecture boundary is violated

---

## 12. Development policy for Codex

Codex should treat this file as the high-level project blueprint.

Before implementation work:

1. Read:
   - root `AGENTS.md`
   - implementation `AGENTS.md`
   - this file
   - the detailed architecture file
   - the goal guide
   - the tutor-style collaboration guide

2. Summarize:
   - the task
   - the applicable milestone
   - fixed constraints
   - the files likely to change
   - the main risks

3. Only then propose or make changes.

By default, Codex should not rely on:
- `1-plan/`
- `3-reference/`

unless the user explicitly requests historical review or reference lookup.

---

## 13. Goal usage policy

When `/goal` is used, it must be used milestone-by-milestone.

Each goal should define:

- objective
- scope
- constraints
- done conditions
- stop conditions
- verification path

Do not use `/goal` for:
- vague project exploration
- product preference decisions
- destructive operations
- rapid prototype tasks that should be handled interactively
- architecture decisions that require human judgment

This aligns with official `/goal` guidance: durable tasks work best when they have a clear target, a validation loop, and enough bounded room for Codex to make progress without needing constant steering. ([developers.openai.com](https://developers.openai.com/codex/use-cases/follow-goals))

---

## 14. Verification policy

No milestone is complete merely because code was generated.

Every milestone should leave behind:

- runnable code or a valid planning artifact
- a concrete verification path
- at least a smoke-check level of validation
- a list of what remains unfinished
- a short note about risks or follow-up work

Preferred verification ladder:

1. import / config sanity
2. local smoke check
3. focused test for the changed behavior
4. operator-readable manual validation notes
5. target-runtime validation where applicable

---

## 15. Coding and agent-working philosophy

This project should be developed under a read-first, reviewable, anti-vibe-coding workflow.

Expected Codex behavior:

- inspect before rewriting
- prefer minimal diffs
- explain the goal before editing
- explain the changed files afterward
- report commands run
- report checks performed
- report remaining risks
- avoid hidden work
- avoid giant one-shot rewrites unless explicitly requested

The human operator should remain able to read, understand, and audit the implementation.

---

## 16. Current implementation order

The preferred immediate order is:

1. scaffold project structure
2. create config and base skeleton
3. add first smoke-test or import/config sanity path
4. initialize the core data/schema layer
5. implement first discovery/input layer
6. implement processing/fetch layer
7. implement transformation/extract layer
8. implement stable storage/versioning
9. implement UI or operator inspection layer
10. implement derived output or analysis layer
11. implement scheduler/worker/runtime persistence
12. stabilize, log, and test
13. only then consider optional assistant/control integration

---

## 17. Success criteria

This project is successful when:

- it can perform its intended domain task continuously or repeatably
- important artifacts are stored in a traceable structure
- metadata/index/state can point to those artifacts
- operators can inspect the system locally
- derived outputs or later-stage processing can be produced where applicable
- the runtime can operate without fragile manual babysitting
- the architecture remains understandable and maintainable

---

## 18. Final note

When this file and the detailed architecture file differ in detail, use this file for:

- project purpose
- milestones
- sequence
- boundaries
- development priorities

Use the detailed architecture file for:

- deeper structural reasoning
- component responsibilities
- implementation-level trade-offs
- data flow specifics