---
name: manage-project-handoff
description: Create, update, inspect, or read a private project session-handoff snapshot so another Codex session or developer can safely continue current work. Use when switching sessions, pausing development, handing off incomplete work, resuming prior progress, or preserving user-specific instructions, constraints, decision rationale, Git state, verification results, blockers, and next steps that could otherwise be lost. Default to docs/private/HANDOFF.md and exclude it from Git. Route durable rules, product requirements, implementation progress, and public behavior to AGENTS.md, PRD, TODO, or README instead of replacing official sources with the handoff.
---

# Manage Project Handoff

Use one private snapshot to preserve immediate context that PRD and TODO do not express. The handoff is a temporary state index, not a second requirements document, TODO, permanent policy, or append-only session log.

## Core Principles

- Read currently active instructions and repository facts first. A handoff never overrides current user direction or project rules.
- Record only verified, still-relevant information required by the next session. Do not copy complete PRDs, TODOs, READMEs, diffs, or conversations.
- Preserve the intent, scope, status, and lifetime of user instructions. Never infer that an instruction is permanent.
- Store the snapshot at `docs/private/HANDOFF.md` by default and exclude `docs/private/` from Git.
- Treat `docs/private/` as accidental-commit protection, not secret storage. Never record tokens, passwords, private keys, or complete sensitive values.
- An ignored local snapshot remains in the current workspace only. For another machine or developer, require a user-selected secure transfer method instead of uploading it to public Git.
- Creating a handoff does not authorize executing next steps, changing official rules, committing, pushing, deleting, or cleaning the worktree.

## Modes and Required References

| Mode | Use when | Read completely |
|---|---|---|
| Prepare handoff | Create, organize, update, or prepare a session handoff | [`references/prepare-handoff_en.md`](references/prepare-handoff_en.md) |
| Resume handoff | A new session needs to understand, inspect, or continue an existing handoff | [`references/resume-handoff_en.md`](references/resume-handoff_en.md) |

If the request says to read and then update, read both references completely in that order. Do not load a reference for an unused mode.

## Route Information to Its Source of Truth

| Information | Official location | Handoff treatment |
|---|---|---|
| Durable project rules that apply across sessions and tasks | `AGENTS.md` | Record as a durable-rule candidate; promote only after explicit user request or confirmation |
| Product problem, goals, scope, requirements, and acceptance | `docs/PRD.md` | Reference the path and necessary IDs without copying the full text |
| Tasks, progress, dependencies, blockers, and implementation next steps | `TODO.md` | Reference related tasks; use `$write-project-todo` first when synchronization is needed |
| Verified public features, commands, and limitations | `README.md`, `README.en.md` | Use `$write-project-readme` first when synchronization is needed |
| Session-only instructions, open questions, uncommitted state, test results, and temporary decisions | `docs/private/HANDOFF.md` | Preserve the minimum snapshot required to continue |
| Credentials or highly sensitive content | Dedicated secret management | Never record it; note only the risk and required action without exposing the value |

Use `$write-project-prd` only when product requirements actually changed and the user requests synchronization. `$manage-project-docs` must not make `HANDOFF.md` public; documentation cleanup should keep the snapshot private by default.

## Record User Instructions

For every instruction that must survive a session change, record:

- **Instruction:** concise wording that preserves intent; retain a necessary short phrase when exact wording matters.
- **Scope:** whole project, feature, file, task, or current work only.
- **Status:** confirmed, current-session only, durable-rule candidate, pending confirmation, or superseded.
- **Source:** for example, “explicit user instruction”; never invent a date, person, or authority.
- **Lifetime or expiry condition:** state that it is unspecified when unknown.
- **Conflict and next-session behavior:** identify differences from existing rules and what the next session should do or avoid.

Reference rather than duplicate content already present in `AGENTS.md`, PRD, TODO, or README. Preserve both sides of a conflict and ask the user to decide instead of merging rules or inferring precedence.

## Minimum Snapshot Content

Include only sections with reliable content:

1. Updated time and timezone, project root, branch, and HEAD.
2. Current objective and scope.
3. User instructions and constraints.
4. Completed work and evidence.
5. Worktree, uncommitted files, and current Git state.
6. Verification performed or not performed and its results.
7. Important decisions, rationale, and still-relevant rejected options.
8. Blockers, risks, and open questions.
9. One to three ordered next actions.
10. Relative paths to required reading and key files.

Never fill gaps with unsupported statements such as “everything complete” or “tests passed.” When no blocker is known, say “no known blocker found” without claiming there is no risk.

## Privacy and Git Boundary

- When preparing a handoff, incrementally ensure `.gitignore` contains a standalone `docs/private/` rule. Never overwrite existing rules or create `docs/private/.gitkeep`.
- Use `git check-ignore` to verify the snapshot is ignored. If it is tracked, stop and report; `.gitignore` does not untrack files or erase history.
- Only when the user explicitly requests public handoff content should you evaluate creating a public document stripped of internal context. Never track `HANDOFF.md` directly.
- Obtain confirmation before deleting or clearing an untracked handoff snapshot because Git usually cannot restore it.

## Completion Report

Prepare Mode reports the snapshot path, sources, synchronized official documents, Git-ignore state, preserved user instructions, open questions, and unverified items. Resume Mode reports the restored objective, active constraints, deviations from current state, trustworthy next steps, and blockers.

Unless the user also asks to continue implementation, Resume Mode only reports state. It does not execute TODO items, edit code, commit, or push automatically.
