---
name: write-project-prd
description: Create, organize, review, or incrementally update docs/PRD.md from user requirements, existing documentation, and the current repository. Define only the product problem, goals, scope, requirements, constraints, and acceptance criteria; do not break work into TODO tasks, write code, or replace detailed technical design with a PRD.
---

# Write Project PRD

Turn known requirements into a clear, verifiable docs/PRD.md suitable for later development. Describe what to build and how completion is evaluated without replacing TODO.md, architecture, API or database design, or implementation work.

## Sources and Information Gaps

Use available context before asking repeated questions. Inspect as applicable:

- Current and prior user requirements
- Existing docs/PRD.md, both README files, and related docs/
- Source code, configuration, tests, issues, specifications, notes, and user-specified sources

When sources conflict:

1. Prefer the user's current explicit instruction.
2. Preserve existing requirements that remain valid.
3. Put unresolved conflicts in Open Questions.
4. Do not silently choose a side or invent a resolution.

Ask only when missing information materially affects the PRD. Prioritize the problem, target users, core features, scope, non-goals, constraints, and completion criteria. Ask at most 3–5 high-value questions at a time. When enough information exists for a useful draft, record remaining gaps in Open Questions instead of inventing requirements.

## Content Principles

- Describe the target product and observable outcomes, not code or implementation details.
- Make requirements specific, understandable, and verifiable; separate confirmed requirements, planned direction, and open questions.
- Do not present suggestions, assumptions, or technical preferences as confirmed product requirements.
- Record material technical constraints, but keep detailed design elsewhere.
- Do not include estimates, checkbox tasks, development phases, or file-by-file implementation steps.
- Do not remove a valid requirement merely because it is not implemented. Claim implementation only when evidence exists and the document explicitly tracks status.
- Select content according to project scale. Do not force business KPIs, complete personas, or irrelevant sections onto small projects.
- Leave no TODO, TBD, template text, empty sections, unsupported numbers, or sensitive information.

## Document Structure

Use only applicable sections:

```markdown
# Product Requirements Document
## Document Information
## Product Overview
## Problem and Background
## Goals
## Non-Goals
## Target Users
## Use Cases
## Functional Requirements
## Non-Functional Requirements
## UX and Interaction Requirements
## Data and Integration Requirements
## Constraints and Dependencies
## Acceptance Criteria
## Success Metrics
## Risks
## Open Questions
## References
```

At minimum, cover the product overview, problem or goals, functional requirements, scope or non-goals, and acceptance criteria. Include Open Questions only when gaps remain.

### Functional Requirements

Use stable IDs for core features:

```markdown
### FR-001: Requirement Name

**Description:** The outcome the feature must provide.

**Acceptance Criteria:**

- An observable and verifiable result.
- Expected behavior for failure or edge cases.
```

- Describe one primary capability per requirement and specify outcomes rather than implementation methods.
- Keep IDs stable after creation; never reuse an ID from a removed requirement.
- Add priorities such as Must, Should, or Could only when useful.

### Non-Functional Requirements and Attribution

Record only known performance, security, privacy, reliability, compatibility, maintainability, accessibility, offline, retention, or backup requirements. Do not invent numeric targets.

When the PRD references, adapts, or is based on another project, repository, paper, tutorial, or specification, record its name, link or source, relationship, and adopted or modified scope in References. Do not treat ordinary dependencies as references automatically.

## Creation and Update Workflow

1. Inspect requirement sources and the current PRD; classify confirmed, conflicting, missing, and assumed information.
2. Ask a few essential questions when necessary; otherwise record gaps as open questions.
3. Select applicable sections and create or incrementally update docs/PRD.md.
4. Validate goals, scope, requirement IDs, references, and acceptance criteria.
5. Report major changes, remaining open questions, and the verification scope.

For initial creation, produce a complete useful draft from known requirements without beginning implementation.

When updating an existing PRD:

- Read it fully and identify added, changed, removed, and conflicting requirements.
- Preserve valid human-written content and stable IDs; update only affected sections.
- Broaden the edit only when restructuring materially improves consistency. Do not rewrite the whole document without need.
- Move cancelled scope to Non-Goals, or remove it explicitly and report the change.

## Completion Check

Before completion, confirm:

- docs/PRD.md exists, is non-empty, is clearly structured, and contains only applicable sections.
- Requirements align with goals, and scope, non-goals, constraints, and dependencies are explicit.
- Core features have stable IDs and observable, verifiable acceptance criteria.
- Confirmed, planned, and open information are separated without obvious conflicts or invented facts.
- No template text, empty sections, implementation tasks, code, or unnecessary technical design remains.
- Existing PRDs were updated incrementally, and references and required attribution were preserved.
- No unrelated files were deleted, secrets exposed, or changes staged, committed, or pushed without explicit instruction.

The completion report must identify the file created or updated, major requirement changes, whether IDs were preserved, unresolved conflicts or questions, references, and that implementation was not started.

The task is complete only after these checks pass and the result is reported.
