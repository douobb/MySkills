---
name: manage-project-docs
description: Inspect, classify, organize, and protect files under a project's docs/ directory. Use for logs, drafts, decisions, specifications, guides, references, and private plans created by Codex or during development. First perform a read-only audit and test whether each file remains understandable without unpublished TODOs, PRDs, or internal TASK, FR, and Phase context. Only verified documents with a defined audience, independent reading value, and a complete publication-gate pass qualify as organized public; rewrite the rest into useful public documentation or default them to private. Delete, merge, move, or update .gitignore only after explicit approval.
---

# Manage Project Documentation

Keep only documentation with lasting value under `docs/`, without treating transient records or internal material as public documentation. Always separate the workflow into a read-only audit and an approval-gated execution phase. Even when the initial request says to organize everything directly, finish the audit and wait for approval first.

## Core Principles

- Follow the project's existing documentation conventions, navigation, naming, and tooling before introducing a new structure.
- Classify from full content, audience, accuracy, references, and long-term value, not filename, age, or length alone.
- Preserve unique context about architectural decisions, constraints, trade-offs, and rationale. Code often shows what exists but not why it was chosen.
- Do not create empty category directories, template documents, or speculative content. A small documentation set may remain directly under `docs/`.
- Evaluate publication suitability separately from writing quality. A polished document is not automatically public.
- Public documentation must remain understandable without ignored, untracked, or private TODOs, PRDs, and internal plans, and must clearly answer who should read it and what value they gain.
- Default a document to private when independent public value cannot be demonstrated. Formal formatting, length, or unique content alone does not justify publication.
- Treat `docs/private/` as protection against accidental commits, not as secure secret storage. Never move tokens, passwords, private keys, or other credentials there as a remedy.
- Treat the `docs/private/` directory pre-created by `$initialize-project-structure` as the standard local privacy boundary. Reuse it when present; never add `.gitkeep` or duplicate the ignore rule.
- Limit the scope to `docs/` unless the user explicitly expands it. Do not organize root READMEs, issues, wikis, or source-code documentation by default.

## Phase One: Read-Only Audit

### 1. Build the inventory

Inspect:

- `AGENTS.md`, READMEs, `.gitignore`, and documentation-tool configuration.
- Every regular and hidden file under `docs/`, including Markdown, text, configuration, images, PDFs, and other document formats.
- Git tracking and ignore state; when available, inspect `git status`, `git ls-files`, and `git check-ignore`.
- Links or references to each target file from READMEs, source code, configuration, and other documentation.
- Duplication, conflicts, version relationships, and likely sources of truth.
- Whether each document depends on ignored, untracked, private, or otherwise unpublished TODOs, PRDs, or other files.
- Undefined internal markers such as `TASK-*`, `FR-*`, `NFR-*`, `DEC-*`, Checkpoint, Sprint, Milestone, Phase, or stage labels.
- Whether content describes implemented and verifiable behavior, an explicitly public roadmap, or an unimplemented internal contract.
- Whether a public document is reachable from a README, documentation index, or another public entry point instead of remaining orphaned.
- Whether `docs/private/` and the exact standalone root `.gitignore` rule `docs/private/` exist. A missing directory may simply mean an empty ignored directory was not preserved by clone, or that a legacy project was never initialized with this boundary.
- Recognize `docs/private/HANDOFF.md` as an operational snapshot managed by `$manage-project-handoff`. It may be inventoried and classified as organized private, but do not propose publishing, moving, or merging it by default.
- Recognize `docs/PRD.md` as the private-by-default official source of `$write-project-prd`. Its publication suitability may be audited, but do not propose publishing, moving, merging, or deleting it without an explicit user request.

Do not follow symbolic links outside the project. Use appropriate tools to read or render supported binary documents. Mark unreadable files as needing confirmation; never classify them as useless without reliable inspection.

### 2. Apply four classifications

| Classification | Criteria | Default action |
|---|---|---|
| Useless | Pure transient logs, duplicate output, or obsolete material with no unique information and no reasonable value to users or future development | Propose deletion, but retain it |
| Needs organization | Contains material worth retaining, but mixes noise, private tracking markers, unverified plans, missing audience context, or dependencies on files that will not be published | Propose a semantic public rewrite when viable; otherwise propose private consolidation |
| Organized public | Clear, accurate, verified, independently understandable, valuable to a defined audience, and passes every publication-gate condition | Keep it or move it to an appropriate public location |
| Organized private | Useful and complete, but its main value depends on internal tracking, product phases, acceptance matrices, commercial considerations, unpublished decisions, or other private context | Propose moving it to `docs/private/` and excluding it from Git |

If a document contains any unique information with continuing value, do not classify it as useless; classify it as needs organization or organized private according to completeness and publication suitability. When accuracy, purpose, or sensitivity is uncertain, state the uncertainty and ask the user to decide.

### 3. Apply the publication gate

Classify a document as organized public only when all conditions below are true:

1. It defines its intended audience, purpose, and what the reader can accomplish or understand afterward.
2. It remains understandable without unpublished TODOs, PRDs, private documents, or internal plans.
3. It contains no undefined internal TASK, FR, NFR, DEC, Checkpoint, Sprint, Milestone, Phase, or stage identifiers.
4. Any retained version, phase, or identifier is defined publicly and provides real value to the reader.
5. It distinguishes current behavior verified by code, tests, configuration, or release information from public limitations and future plans; it never presents an unimplemented contract as an existing capability.
6. It reveals no private product strategy, commercial considerations, internal acceptance relationships, or security-sensitive information.
7. It is discoverable from a README, public index, or another public document and includes required cross-links.
8. It has continuing maintenance value for users or new developers, rather than merely proving what Codex, one task, or one development phase did.

If any condition fails, the document is not organized public. Classify it as needs organization when it can be rewritten into an independent and useful public document without exposing private context. Classify it as organized private when removing that context would destroy its primary value. When independent public value cannot be demonstrated, default to organized private.

### 4. Report and stop

List every file under one of the four classifications. For each file, report at least:

- Relative path.
- A one- or two-sentence summary; use a high-level summary that does not disclose details for sensitive files.
- Classification and rationale, including publication-gate pass and failure items.
- Dependencies on private or unpublished files, plus undefined internal tracking markers.
- Tracked, untracked, or ignored Git state.
- Proposed action, destination, and main risks.

Also provide:

- The exact files proposed for deletion.
- For every merge, the source files, target file, content to retain, and disposition of each source.
- For every file that needs organization, evaluate both semantic public rewriting and private consolidation, recommend one, and list failed gate conditions when a public rewrite is not viable.
- The smallest proposed `docs/` structure, listing only directories needed for this task.
- Proposed `.gitignore` additions or corrections.
- Conflicts, sensitivity questions, or factual uncertainty that require user judgment.

Stop after the report. In this phase, report a missing privacy boundary only as a compatibility issue. Until the user explicitly approves the exact deletion, merge, move, and Git-change plan, do not create directories, update `.gitignore`, move, rewrite, or delete anything. Partial approval authorizes only the explicitly approved items.

## Phase Two: Execute the Approved Plan

### 1. Recheck current state

Before editing, verify that every approved file is unchanged and still exists at the expected path. If the audit is stale, a new conflict appears, or scope has changed, stop and revise the plan instead of applying stale conclusions.

### 2. Organize public documentation

Existing conventions take precedence. When none exist, select only the locations justified by actual content:

```text
docs/
├── tutorials/              # Guided learning experiences
├── guides/                 # Goal-oriented how-to guides
├── reference/              # APIs, configuration, schemas, and precise facts
├── explanation/            # Background, concepts, principles, and trade-offs
├── architecture/           # System architecture and design
│   └── decisions/          # ADRs and significant decision records
├── operations/             # Deployment, operations, troubleshooting, and runbooks
└── assets/                 # Images and attachments used by documentation
```

Create a directory only when at least one approved document will occupy it. Do not over-nest a small project. Where practical, make reference documentation mirror the structure of the system it describes. Create or update `docs/README.md` or an index only when it materially improves navigation; never create an empty index.

Public organization is not mechanical identifier removal. When performing a public rewrite:

1. Define the intended audience, purpose, scope, and current status first.
2. Replace tracking statements such as `maps to TASK-003` with independently understandable domain meaning, such as “This section defines Session state transitions,” instead of merely deleting the identifier.
3. Convert an internal Phase into a publicly defined version or capability status only when readers need it; otherwise move it to private documentation.
4. Describe current behavior only when supported by code, tests, configuration, or formal release information. Keep unverified specifications private or place them explicitly in a published roadmap.
5. Create the smallest useful public projection from private sources without copying private acceptance relationships, schedules, commercial context, or unnecessary detail.
6. Add required background, terminology, and public links, then create an entry point from a README or public index.
7. Reapply the publication gate. If any condition still fails, move the document to private instead of forcing publication.

### 3. Organize private documentation

- Default internal product phases, TASK or FR traceability, acceptance matrices, Codex work evidence, and complete specifications that cannot be understood without private PRDs or TODOs to private documentation.
- Prefer the `docs/private/` directory and exact standalone root `.gitignore` rule `docs/private/` created during initialization. When both are correct, reuse them without rewriting anything.
- If the rule exists but the directory is absent after a clone or in an older workspace, create the directory only when an approved private document actually needs a destination. Do not create it merely to complete an empty structure.
- If the directory or exact ignore rule is missing, create or add it incrementally only within the user-approved plan. Preserve existing `.gitignore` content and never duplicate the rule.
- Do not create `docs/private/.gitkeep`; the directory itself must not be committed.
- Treat `docs/private/HANDOFF.md` as the reserved operational snapshot of `$manage-project-handoff`. Unless the user explicitly includes it in this task, do not rewrite, merge, move, or delete it; delegate content updates to the handoff skill.
- Treat `docs/PRD.md` as the reserved official source of `$write-project-prd`; keep its path and standalone ignore rule by default. Unless the user explicitly includes it in scope and approves updating every consumer, do not rewrite, publish, merge, move, or delete it.
- `.gitignore` does not affect tracked files. Report the exact private files already tracked by Git, and change the index only when the user explicitly approves untracking them.
- If content was pushed previously, explain that adding an ignore rule does not remove Git history. Never rewrite history, force-push, or claim remote removal automatically.
- If real credentials or highly sensitive data are found, stop moving and summarizing them, do not echo their values, and recommend revocation or rotation. Never present `docs/private/` as an adequate remedy.

### 4. Merge and clean up

For every approved plan:

1. Create or update the destination first, preserving all accurate and unique information, rationale, constraints, and required attribution.
2. Remove duplication, stale records, conversational fragments, and unsupported conclusions without inventing replacement facts.
3. Normalize audience, terminology, headings, filenames, and relative links.
4. Verify that the destination is complete enough to replace its sources.
5. Update affected READMEs, indexes, configuration, and cross-references.
6. Only then dispose of approved source files. Delete only exact approved paths; warn before deleting untracked files that Git may not recover, and prefer a recoverable method when practical.

Do not change product requirements, program behavior, or technical decisions while organizing documentation. Preserve and report conflicting claims instead of deciding silently.

## Completion Verification and Report

Before completion, verify:

- Every original document has a final classification or an explicit unresolved status.
- Every deletion, merge, move, and Git change is within the approved scope.
- Every public document passes all publication-gate conditions, provides clear reader value, and has a public entry point.
- No public document depends on ignored, untracked, private, or otherwise unpublished files.
- Public documentation contains no identified private planning, credentials, or unnecessary internal records.
- TASK, FR, NFR, DEC, Checkpoint, Sprint, Milestone, Phase, and stage markers were scanned; only publicly defined identifiers useful to readers remain.
- The privacy boundary was reused or repaired within the approved plan, `docs/private/` is ignored without duplicate rules, and exceptions for tracked files are disclosed accurately.
- `docs/private/HANDOFF.md` remains private and was not rewritten, merged, moved, or deleted without authorization.
- `docs/PRD.md` remains the official private-by-default source, or its publication or move was explicitly authorized and every reference was synchronized.
- No empty category directories, duplicate documents, or blank indexes were created.
- Relative links, images, documentation navigation, and major references still work after moves.
- `git status` contains only expected changes; nothing was staged, committed, or pushed automatically.

Finally list every retained, created, merged, moved, and deleted file; updated links and `.gitignore` rules; unresolved items; and the Git-tracking and remote-history risks for private documents.

## Design References

- [Diátaxis](https://diataxis.fr/start-here/): distinguishes tutorials, how-to guides, reference, and explanation by reader need; use only categories that add value.
- [Git `gitignore` documentation](https://git-scm.com/docs/gitignore): ignore rules affect untracked files and do not erase existing tracking or remote history.
- [Documentation and ADRs Skill](https://github.com/addyosmani/agent-skills/blob/main/skills/documentation-and-adrs/SKILL.md): preserve decision context, constraints, and trade-offs, and match existing conventions first.