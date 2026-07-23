---
name: manage-project-docs
description: Inspect, classify, organize, and protect files under a project's docs/ directory. Use for logs, drafts, decision records, guides, references, and private plans created by Codex or during development. First perform a read-only audit that summarizes every file and classifies it as useless, needs organization, organized public, or organized private. Delete, merge, move, create docs/private/, or update .gitignore only after the user explicitly approves the exact plan.
---

# Manage Project Documentation

Keep only documentation with lasting value under `docs/`, without treating transient records or internal material as public documentation. Always separate the workflow into a read-only audit and an approval-gated execution phase. Even when the initial request says to organize everything directly, finish the audit and wait for approval first.

## Core Principles

- Follow the project's existing documentation conventions, navigation, naming, and tooling before introducing a new structure.
- Classify from full content, audience, accuracy, references, and long-term value, not filename, age, or length alone.
- Preserve unique context about architectural decisions, constraints, trade-offs, and rationale. Code often shows what exists but not why it was chosen.
- Do not create empty category directories, template documents, or speculative content. A small documentation set may remain directly under `docs/`.
- Evaluate publication suitability separately from writing quality. A polished document is not automatically public.
- Treat `docs/private/` as protection against accidental commits, not as secure secret storage. Never move tokens, passwords, private keys, or other credentials there as a remedy.
- Limit the scope to `docs/` unless the user explicitly expands it. Do not organize root READMEs, issues, wikis, or source-code documentation by default.

## Phase One: Read-Only Audit

### 1. Build the inventory

Inspect:

- `AGENTS.md`, READMEs, `.gitignore`, and documentation-tool configuration.
- Every regular and hidden file under `docs/`, including Markdown, text, configuration, images, PDFs, and other document formats.
- Git tracking and ignore state; when available, inspect `git status`, `git ls-files`, and `git check-ignore`.
- Links or references to each target file from READMEs, source code, configuration, and other documentation.
- Duplication, conflicts, version relationships, and likely sources of truth.

Do not follow symbolic links outside the project. Use appropriate tools to read or render supported binary documents. Mark unreadable files as needing confirmation; never classify them as useless without reliable inspection.

### 2. Apply four classifications

| Classification | Criteria | Default action |
|---|---|---|
| Useless | Pure transient logs, duplicate output, or obsolete material with no unique information and no reasonable value to users or future development | Propose deletion, but retain it |
| Needs organization | Mixes useful content with noise, overlaps other documents, contains fragmented information, or has an unclear location or audience | Propose sources, destination, and merge plan |
| Organized public | Clear and accurate for its intended audience, contains nothing that should remain private, and is maintainable as public documentation | Keep it or move it to an appropriate public location |
| Organized private | Useful and complete, but contains internal product plans, commercial considerations, unpublished decisions, or other material unsuitable for publication | Propose moving it to `docs/private/` and excluding it from Git |

If a document contains any unique information with continuing value, do not classify it as useless; classify it as needing organization. When accuracy, purpose, or sensitivity is uncertain, state the uncertainty and ask the user to decide.

### 3. Report and stop

List every file under one of the four classifications. For each file, report at least:

- Relative path.
- A one- or two-sentence summary; use a high-level summary that does not disclose details for sensitive files.
- Classification and rationale.
- Tracked, untracked, or ignored Git state.
- Proposed action, destination, and main risks.

Also provide:

- The exact files proposed for deletion.
- For every merge, the source files, target file, content to retain, and disposition of each source.
- The smallest proposed `docs/` structure, listing only directories needed for this task.
- Proposed `.gitignore` additions or corrections.
- Conflicts, sensitivity questions, or factual uncertainty that require user judgment.

Stop after the report. Until the user explicitly approves the exact deletion, merge, move, and Git-change plan, do not create directories, update `.gitignore`, move, rewrite, or delete anything. Partial approval authorizes only the explicitly approved items.

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

### 3. Organize private documentation

- Place approved organized private documents under `docs/private/`, and keep an exact standalone `docs/private/` rule in the repository-root `.gitignore`.
- Do not create `docs/private/.gitkeep`; the directory itself must not be committed.
- Preserve all existing `.gitignore` content and add only missing rules without duplication.
- If `docs/PRD.md` is a fixed input for existing skills, scripts, or workflows, it may remain in place with its own ignore rule. Do not move it unless the user approves updating every consumer.
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
- Public documentation contains no identified private planning, credentials, or unnecessary internal records.
- `docs/private/` is ignored and exceptions for tracked files are disclosed accurately.
- No empty category directories, duplicate documents, or blank indexes were created.
- Relative links, images, documentation navigation, and major references still work after moves.
- `git status` contains only expected changes; nothing was staged, committed, or pushed automatically.

Finally list every retained, created, merged, moved, and deleted file; updated links and `.gitignore` rules; unresolved items; and the Git-tracking and remote-history risks for private documents.

## Design References

- [Diátaxis](https://diataxis.fr/start-here/): distinguishes tutorials, how-to guides, reference, and explanation by reader need; use only categories that add value.
- [Git `gitignore` documentation](https://git-scm.com/docs/gitignore): ignore rules affect untracked files and do not erase existing tracking or remote history.
- [Documentation and ADRs Skill](https://github.com/addyosmani/agent-skills/blob/main/skills/documentation-and-adrs/SKILL.md): preserve decision context, constraints, and trade-offs, and match existing conventions first.