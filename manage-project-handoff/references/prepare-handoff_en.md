# Prepare a Handoff

Run this procedure when the user asks to create, update, or prepare a session handoff.

## 1. Confirm Scope and Sources

Read currently active `AGENTS.md`, any existing `docs/private/HANDOFF.md`, `TODO.md`, `docs/PRD.md`, READMEs, and code or documents directly related to current work. Inspect the Git root, branch, HEAD, staged/unstaged/untracked files, active Git operations, and verification performed during current work.

Use only facts supported by the current conversation, repository, tool results, and existing documents. Mark unverifiable content from an old handoff as stale or pending confirmation instead of treating it as current.

## 2. Route User Instructions

Identify each explicit instruction:

1. Already in an official source: reference its source and relevant location only.
2. Limited to current work or a specific task: preserve it in the snapshot with scope and expiry.
3. Potentially durable: list it as an `AGENTS.md` candidate and wait for user confirmation. Until confirmed, transmit it through the handoff without editing `AGENTS.md`.
4. Product requirement or implementation state: route it to PRD or TODO as defined by the main skill.
5. Conflicts with an existing rule: preserve both statements, sources, and impact; do not promote or merge them automatically.

Never present an assistant-chosen method as a user instruction. Mark an instruction inferred only from context as “inferred, pending confirmation” or omit it.

## 3. Synchronize Official Sources

- When implementation progress, next actions, or blockers changed, use `$write-project-todo` to update the local TODO.
- When verified public behavior, commands, configuration, or limitations changed, use `$write-project-readme` to synchronize both READMEs.
- Use `$write-project-prd` only when product requirements changed and the user requests an update.
- Update `AGENTS.md` only after explicit confirmation that a rule is durable.

After another skill edits files, recheck Git state and affected facts. The handoff must not trigger code implementation by itself.

## 4. Establish the Private Boundary

1. Follow an existing private-document convention; otherwise use `docs/private/HANDOFF.md`.
2. Incrementally create `docs/private/` and ensure the root `.gitignore` contains a standalone `docs/private/` rule.
3. Check whether the target is tracked or appeared in commit history. If tracked, stop and report untracking and history risks without changing the index.
4. After writing, verify with `git check-ignore -v docs/private/HANDOFF.md`.
5. If the recipient does not share the current workspace, confirm a user-selected secure transfer method. Without one, report the limitation and do not publish or stage the handoff.

When credentials or highly sensitive values appear, do not copy or summarize them. Record only the risk category and the need to revoke, rotate, or remove them from the project.

## 5. Update One Snapshot

Update incrementally instead of appending a new session section:

- Preserve constraints, decisions, blockers, and next steps that remain correct.
- Refresh branch, HEAD, worktree, and verification state from current evidence.
- Remove clearly expired or superseded temporary content; retain concise rationale when it still affects later decisions.
- Replace extensive detail with relative paths, task IDs, or commit references.
- Limit next steps to one to three directly actionable items ordered by dependency.

Use a verifiable current time and timezone. Never invent a session ID, completion date, test result, or owner.

## 6. Validate and Report

Confirm that someone absent from the prior session can understand the objective, constraints, state, and starting point; paths exist or are marked not yet created; Git and verification results match current state; user instructions include scope, status, source, and lifetime; the snapshot is ignored and not staged/tracked; and it contains no secrets, complete diff, complete PRD/TODO, or lengthy conversation copy.

Finally report the path, synchronized official sources, ignore verification, durable-rule candidates, open questions, and recommended reading order for the next session.
