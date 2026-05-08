# architecture-design.md

## 1. File role

This file is the detailed architecture anchor.

Its job is not to replace the root `AGENTS.md`.
Its job is not to replace `project-overview-and-plan.md`.
Its job is not to define `/goal` usage discipline.

Its job is to answer:

- how the system should be layered internally
- what each layer is responsible for
- what each layer is explicitly not responsible for
- how data and state should move across the system
- what implementation boundaries must be preserved

If this file conflicts with higher-level files, use this precedence:

1. root `AGENTS.md`
2. `4-implementation/AGENTS.md`
3. `project-overview-and-plan.md`
4. this file

---

## 2. Relation to repository structure

This file belongs in the active authoritative non-code instruction area:

- `2-action/sources/`

Current implementation work should normally prefer these inputs:

- root `AGENTS.md`
- `4-implementation/AGENTS.md`
- `2-action/sources/project-overview-and-plan.md`
- `2-action/sources/architecture-design.md`
- `2-action/sources/goal-guide.md`
- `2-action/sources/tutor-prompt.md`

The following directories are historical by default and should not be treated as active implementation truth unless explicitly requested:

- `1-plan/`
- `3-reference/`

---

## 3. Architecture purpose

This project should be implemented as a layered engineering system, not as a pile of prompt-driven file edits.

The architecture must support:

1. clear responsibilities
2. low coupling between layers
3. testable stage-by-stage growth
4. inspectable state and outputs
5. safe long-horizon Codex work
6. human reviewability at every stage

This is especially important for long tasks, because durable agent workflows perform better when the objective, boundaries, and validation model are explicit. ([developers.openai.com](https://developers.openai.com/codex/use-cases/follow-goals) :contentReference[oaicite:1]{index=1})

---

## 4. System-wide layer model

Every project using this structure should think in layers.

The generic layer model is:

1. Intake / Discovery layer
2. Processing / Fetch layer
3. Transformation / Extract layer
4. Storage / Artifact layer
5. Metadata / Index / State layer
6. Analysis / Derived-output layer
7. UI / API / Operator layer
8. Runtime / Scheduling / Worker layer
9. Optional assistant / control layer

Not every project needs every layer in full.
But if a layer exists, its responsibility should be explicit.

### Core boundary principles

The following boundary style should always be preserved:

- discovery is not processing
- processing is not transformation
- transformation is not analysis
- UI is not scheduler
- scheduler is not business logic
- metadata is not the primary artifact store
- assistant layer is not automatically the production runtime

---

## 5. Intake / Discovery layer

### 5.1 Responsibility

This layer is only responsible for finding or accepting candidate work items.

Examples may include:
- URLs
- files
- messages
- tasks
- structured inputs
- user-supplied records

### 5.2 What it should output

It should output lightweight candidate items with just enough information to hand off to the next stage, for example:

- identifier
- source type
- time discovered
- intake method
- initial status

### 5.3 What it should not do

It should not:
- perform deep processing
- do final transformation
- act like the UI layer
- hide errors from later stages
- absorb unrelated runtime logic

### 5.4 Design reason

This keeps the “finding work” step cheap, simple, and easy to verify.

---

## 6. Processing / Fetch layer

### 6.1 Responsibility

This layer is responsible for obtaining the primary raw input needed by the system.

Examples:
- fetching a page
- loading a file
- requesting an API
- reading a message body
- retrieving source payloads

### 6.2 What it should output

It should output raw artifacts or raw payloads plus status metadata such as:

- raw content
- status/result
- time processed
- error information if failed
- raw artifact path where applicable

### 6.3 What it should not do

It should not:
- pretend raw content is already clean content
- mix in analysis logic
- bury retry/scheduling policy inside core processing
- silently drop failures

### 6.4 Design reason

This preserves a raw evidence layer.
Later stages should be able to reprocess or re-extract from raw inputs if needed.

---

## 7. Transformation / Extract layer

### 7.1 Responsibility

This layer converts raw inputs into normalized, cleaner, structured, or more usable outputs.

Examples:
- raw HTML → cleaned markdown
- raw text → normalized text
- external payload → internal schema
- source artifact → structured fields

### 7.2 What it should output

Typical outputs:
- cleaned artifact
- normalized artifact
- extracted metadata
- transformation status
- output path or structured representation

### 7.3 What it should not do

It should not:
- overwrite the raw evidence layer
- act as the scheduler
- act as the UI
- quietly swallow quality failures

### 7.4 Design reason

Keeping transformation separate makes it easier to:
- debug quality problems
- improve extractors later
- preserve provenance
- rerun later stages without refetching

---

## 8. Storage / Artifact layer

### 8.1 Responsibility

This layer defines where real content or generated artifacts live.

Examples:
- raw artifacts
- cleaned artifacts
- derived outputs
- reports
- generated files
- logs

### 8.2 General rule

The artifact store should be explicit and inspectable.

Typical pattern:
- raw artifacts in one area
- cleaned/normalized artifacts in another
- derived outputs in another
- logs in another

### 8.3 What it should not do

It should not:
- collapse unrelated artifact classes into one flat area
- rely on vague path rules
- hide provenance
- let metadata storage replace artifact storage

### 8.4 Design reason

This makes debugging, backup, reprocessing, and operator inspection much simpler.

---

## 9. Metadata / Index / State layer

### 9.1 Responsibility

This layer stores compact structured state, not primary artifact bodies.

Examples:
- identifiers
- statuses
- timestamps
- paths
- relationships
- tags
- counters
- run history
- retrieval pointers

### 9.2 Typical structures

Depending on the project, this may include things such as:
- sources
- items/documents
- versions
- runs/jobs
- tags
- statuses

### 9.3 What it should not do

It should not become:
- the primary full-body artifact store
- the hidden business-logic layer
- the replacement for on-disk provenance

### 9.4 Design reason

The metadata layer should stay small, structured, and easy to query.

---

## 10. Analysis / Derived-output layer

### 10.1 Responsibility

This layer produces secondary outputs from already normalized or stored content.

Examples:
- summaries
- tags
- classifications
- improved text
- structured notes
- enrichment data
- later-stage inference artifacts

### 10.2 What it should output

It should produce:
- derived artifacts
- versionable outputs where practical
- explicit metadata linkage to the source item

### 10.3 What it should not do

It should not:
- overwrite raw evidence by default
- replace the main processing pipeline
- hide prompt/model/template decisions if AI is involved
- collapse all derived work into one opaque step

### 10.4 Design reason

Derived outputs should remain inspectable, versionable, and replaceable.

---

## 11. UI / API / Operator layer

### 11.1 Responsibility

This layer is for human or external-system interaction.

Examples:
- local web UI
- API endpoints
- admin actions
- inspection pages
- safe narrow triggers

### 11.2 What it should do

It should:
- expose state clearly
- show artifacts and metadata
- enable safe narrow actions
- remain thin and delegate real work to services

### 11.3 What it should not do

It should not:
- become the scheduler host
- bury core processing logic inside handlers
- hide long-running loops in request paths
- replace explicit runtime design

### 11.4 Design reason

Keeping UI thin makes the system easier to reason about and more stable under growth.

---

## 12. Runtime / Scheduling / Worker layer

### 12.1 Responsibility

This layer is responsible for how work is dispatched and executed over time.

Typical responsibilities:
- scheduler
- worker
- retry rules
- persistence/restart behavior
- long-running services
- bounded background execution

### 12.2 Scheduler role

The scheduler should:
- create or dispatch work
- not absorb all business logic

### 12.3 Worker role

The worker should:
- execute defined stages
- report statuses and failures
- respect scope and boundaries

### 12.4 What it should not do

It should not:
- quietly merge with UI logic
- become an invisible background loop hidden somewhere random
- act like a substitute for architecture

### 12.5 Design reason

Explicit runtime roles make long-running systems more stable and auditable.

---

## 13. Optional assistant / control layer

### 13.1 Responsibility

This layer is optional.

Possible responsibilities:
- safe remote trigger
- narrow command interface
- operator query interface
- assistant-style inspection

### 13.2 What it should not become

It should not automatically become:
- the main production runtime
- the scheduler
- the primary business logic owner
- the hidden control plane for everything

### 13.3 Design reason

Assistant/control interfaces are useful, but they should stay outside the core runtime unless explicitly designed otherwise.

---

## 14. Data flow philosophy

The system should be understandable as a pipeline.

A common generic path is:

```text
candidate item
→ raw input
→ cleaned/normalized output
→ stored artifact
→ metadata/state update
→ derived output
→ UI/operator visibility
```

The exact names vary by project, but the flow should remain explicit.

### Required properties

The data flow should preserve:

- provenance
- layer separation
- visible failure states
- rerun capability
- operator-readable status

------

## 15. Failure visibility philosophy

Failures must not disappear into vague logs or hidden retries.

Every important stage should make it possible to answer:

- what input failed
- at which stage it failed
- whether it can be retried
- what artifact/state was produced before failure
- what remains unprocessed

This is important both for human review and for long-horizon Codex tasks, where verification has to stay explicit. ([developers.openai.com](https://developers.openai.com/blog/run-long-horizon-tasks-with-codex) ([OpenAI Developers](https://developers.openai.com/blog/run-long-horizon-tasks-with-codex)))

------

## 16. Versioning philosophy

Whenever a project can produce multiple later-stage outputs from one canonical item, prefer version-aware design.

Typical examples:

- multiple summaries
- improved rewrites
- manual edits
- repeated analyses
- alternate derived forms

Version-aware design helps preserve:

- provenance
- auditability
- rollback ability
- comparison across generations

------

## 17. Current engineering constraints mindset

Implementation under this architecture must preserve these working habits:

- build the smallest useful skeleton first
- stabilize one layer before expanding complexity
- make boundaries explicit before automating them
- preserve auditability over “looks complete”
- prefer readable, reviewable changes
- do not confuse current-machine authoring checks with target-runtime validation
- do not assume Codex exists in every environment unless explicitly stated

------

## 18. Codex implementation discipline

When Codex reads this file, it should follow this implementation discipline:

1. read current authoritative files first
2. understand which layer the task belongs to
3. avoid cross-layer confusion
4. prefer minimal changes
5. explain the architecture role of the changed code
6. accompany changes with verification
7. report risks and unfinished areas
8. stop if architecture drift would be required

For complex work, plan first and move milestone by milestone. This is consistent with official Codex best practices. ([developers.openai.com](https://developers.openai.com/codex/learn/best-practices) ([OpenAI Developers](https://developers.openai.com/codex/learn/best-practices)))

------

## 19. Recommended implementation order

A safe generic order is:

1. project skeleton and config layer
2. core data/schema/init layer
3. first input/discovery layer
4. processing/fetch layer
5. transformation/extract layer
6. storage/versioning linkage
7. UI/operator inspection layer
8. analysis/derived-output layer
9. runtime/scheduler/worker persistence
10. testing/logging/stabilization
11. optional assistant/control integration

Do not reverse this order casually.
Do not front-load advanced assistant/control work before the main runtime is stable.

------

## 20. Final note

This file is the detailed architecture anchor.

Use it for:

- structural reasoning
- layer responsibilities
- boundary preservation
- data flow understanding
- implementation-level trade-offs

Use the project overview file for:

- milestone order
- success criteria
- high-level project identity
- development sequence

Use the goal guide for:

- `/goal` structure
- stop conditions
- final report requirements
- milestone-by-milestone automation discipline