---
name: write-project-todo
description: Create, organize, review, or incrementally update a local project implementation plan from docs/PRD.md, the current repository, and an existing TODO.md. Use to break down requirements, order phases and dependencies, and track next steps, blockers, and progress; do not change product requirements, implement features, or execute TODO tasks automatically.
---

# Write Project TODO

Convert the PRD and current project state into an actionable, ordered, and verifiable TODO.md that manages what to do next. Do not replace the PRD, technical design, or implementation work, and do not automatically add the local TODO.md to version control.

## Sources and Priority

Inspect as applicable:

- docs/PRD.md and the existing TODO.md
- Both README files, docs/, issues, and change records
- Source code, tests, configuration, and package manifests
- Git status and recent changes when safely available
- The user's current explicit instruction

When sources conflict, prefer:

1. The user's current explicit instruction
2. Valid PRD requirements
3. Current state proven by code, tests, and configuration
4. Existing TODO.md
5. Other documentation and historical information

Do not resolve uncertain conflicts by assumption. Put them in Open Questions and report them. When the PRD is missing or insufficient, create only a limited plan from reliable information and state the gaps instead of inventing requirements.

## Planning Principles

- Convert PRD requirements into implementation work rather than copying PRD headings into checkboxes.
- Give every task a clear outcome and an observable or executable completion method.
- Order work by real dependencies and prioritize foundational tasks that remove blockers.
- Check for circular dependencies. If a cycle exists, do not produce an impossible ordering; revise the breakdown or record the cycle as a blocker.
- Include testing, documentation, security, integration, and release preparation when appropriate.
- Do not write code, modify docs/PRD.md, create detailed architecture, API, or database designs, or execute tasks automatically.
- Do not add guessed estimates, invented progress or test results, secrets, template text, empty phases, or meaningless tasks.

## Tasks and Phases

### Task Granularity

Keep each task completable in one reasonably focused development effort. Split tasks with independent outcomes, multiple system layers, or no single validation method. Do not reduce work to individual files, functions, or command executions.

Too large:

```markdown
- [ ] Complete the user system
```

Appropriate:

```markdown
- [ ] Create the user data model and migration
- [ ] Implement login and logout flows
- [ ] Add session validation and expiration handling
- [ ] Add tests for failed login and expired sessions
```

### Task Format

For small tasks:

```markdown
- [ ] Task name
```

For central or dependent tasks:

```markdown
- [ ] TASK-001 Task name
  - Requirement: FR-001
  - Depends on: TASK-000
  - Validation: Observable or executable completion check
```

- Assign one primary outcome per task, and never use “verify it works” as the complete validation description.
- Preserve TASK IDs after creation when possible, and never reuse an ID from a removed task.
- Record only real dependencies, and do not add full metadata to every minor task.

### Phases and Document Structure

Order phases with clear goals and completion boundaries by dependency, such as foundation, core data and services, main features, integration and error handling, quality, and release preparation. Add checkpoints to complex phases. Use a flat task list for small projects rather than forcing a fixed phase model.

Use only applicable sections:

```markdown
# Project Implementation Plan

## Current Status
- Current phase:
- Next step:
- Blockers:

## Phase 1: Name
**Goal:**
- [ ] Task

## Cross-Phase Work
## Open Questions
## Cancelled or Deferred Items
```

Do not create empty sections. Include a progress percentage only when it can be calculated reliably from task states.

## Completion Status

Use [ ] for incomplete and [x] for complete. Mark [x] only when implementation matches the task scope and credible evidence comes from relevant tests, builds, documentation, validation, or explicit user confirmation. A file's existence alone does not prove completion.

Keep partial or unverifiable work unchecked and record Status, Completed, and Remaining details when useful.

**Completing a TASK does not mean its FR is accepted.** Report an FR as accepted only when evidence satisfies every applicable acceptance criterion in the PRD. Never infer overall requirement completion from one task's state.

## Creation and Update Workflow

1. Inspect the PRD, current TODO, and repository; classify requirements, completed capabilities, gaps, and blockers.
2. Break incomplete requirements into appropriately sized tasks and map them to requirements.
3. Order dependencies and phases, checking for cycles and tasks that cannot start.
4. Add necessary quality work and create or incrementally update TODO.md.
5. Validate task status, requirement mapping, completion methods, next steps, and blockers.
6. Report major changes and the recommended next step without starting implementation.

For initial creation, produce a complete useful draft from reliable information.

When updating an existing TODO:

- Read it fully and preserve valid phases, tasks, and IDs.
- Add or adjust tasks based on changes in the PRD, code, tests, and configuration.
- Update completion only with evidence, and move cancelled or deferred work to the appropriate section.
- Refresh the current phase, next step, and blockers without unnecessarily rewriting, renumbering, or reordering the document.

## Completion Check

Before completion, confirm:

- TODO.md exists, is non-empty, and maps tasks to PRD requirements, current gaps, or necessary quality work.
- Tasks have appropriate granularity and clear outcomes, and central tasks have determinable completion methods.
- Phases and tasks follow dependencies, with no unresolved circular dependency.
- Every [x] has credible evidence, and partial work is not incorrectly marked complete.
- TASK and FR status are evaluated separately; one completed task is not reported as an accepted requirement.
- Next steps, blockers, cancellations, and deferrals match current state.
- Existing TODO content was updated incrementally and contains no code, unsupported facts, secrets, template text, or empty sections.
- No unrelated file was deleted and no changes were staged, committed, or pushed without explicit instruction.

The completion report must summarize major tasks added, changed, completed, cancelled, or deferred; whether IDs were preserved; the current phase, next step, blockers, and open questions; and that implementation was not started.

The task is complete only after these checks pass and the result is reported.
