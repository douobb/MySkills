---
name: manage-project-git
description: Manage project Git initialization, commits, and pushes safely with risk-based depth. Use for a first git init, initial branch and remote setup, and the initial commit, or for inspecting an existing repository, synchronizing documentation, scanning sensitive information and extraneous files, verifying, staging exact paths, committing, and uploading. Use Normal Mode for low-risk changes, Enhanced Mode for initialization or unfamiliar and high-risk content, and Stop Mode for version differences, conflicts, failures, secrets, or mixed staged content so the user can choose the resolution.
---

# Manage Project Git

Load a sufficient, non-redundant procedure based on risk. This main file defines mode selection and shared baselines; complete procedures live under `references/`.

## Core Principles

- Determine whether the request is initialization only, commit only, push only, or commit and push. Do not expand the external change.
- An explicit “upload” request authorizes normal staging, commit, and non-force push after checks pass; do not ask again at every normal stage.
- Limit work to the current scope. Preserve unrelated modifications, branches, tags, remotes, and staged state; stage exact paths only.
- Scanning reduces risk but never proves no secret exists. Never echo complete secret values.
- Never automatically run `reset --hard`, `clean`, discard changes, delete branches, `commit --amend`, rewrite history, or force-push.

## Select the Workflow and Mode

Resolve the Git root first. Use Workflow A when it is not a repository or first-time initialization was requested; otherwise use Workflow B. Clarify scope for nested repositories, submodules, worktrees, or an ambiguous target.

| Mode | Conditions |
|---|---|
| Normal | Existing repository; small, single-purpose text or source changes; known remote and upstream; no abnormal staged content or high-risk signal |
| Enhanced | First initialization; many or unfamiliar untracked files; binary, large, or generated files; environment, authentication, or private documentation; broad or high-risk code; mixed-purpose changes; unreviewed outgoing commits; unclear remote or upstream |
| Stop | Possible secret; unrelated pre-existing staged content; detached HEAD; active Git operation; conflicts; material failed verification; remote mismatch; local behind or diverged state; authentication, permission, hook, or push error |

Use the highest-risk applicable mode. Do not select Enhanced merely because one untracked file exists; consider count, type, source, and task relationship. For inspection or preparation only, stop after the pre-commit report.

## Required References

After selecting a mode, read its file completely before mode-specific checks or any action that changes Git state:

- Normal Mode: [`references/normal-mode_en.md`](references/normal-mode_en.md)
- Enhanced Mode or Workflow A: [`references/enhanced-mode_en.md`](references/enhanced-mode_en.md)
- Any stop condition: stop expanding impact immediately and read [`references/stop-mode_en.md`](references/stop-mode_en.md) completely before reporting.

References are not optional summaries. If the mode changes, read the new mode file first. Do not load references for untriggered modes.

## Shared Safety and Documentation Baseline

At minimum, inspect for `.env`, credentials, private keys, cloud authentication, cookies, sessions, connection strings, credential-bearing URLs, API keys, tokens, passwords, personal or customer data, internal endpoints, commercial plans, unpublished PRDs or TODOs, and `docs/private/`. A possible secret switches immediately to Stop Mode.

Invoke other available skills when applicable:

- Verified features, commands, configuration, limitations, versions, or structure changed: use `$write-project-readme`.
- `docs/` contains development records, duplication, or private content: use `$manage-project-docs`; pause Git when it requires approval.
- Local `TODO.md` status changed: use `$write-project-todo`, keep it ignored, and do not upload it merely because it was synchronized.
- Product requirements changed and the user requests an update: use `$write-project-prd`; keep the PRD private and ignored by default.
- An empty directory also needs a scaffold: use `$initialize-project-structure`, then return to Workflow A.
- Broad or high-risk code needs pre-delivery review: use `$code-review` for read-only findings.

Run only existing repository checks relevant to the change. Run `git diff --check` and, before committing, `git diff --cached --check`. Do not install dependencies, change the toolchain, or use `--no-verify` to hide errors.

## Workflow Routing and Check Invalidation

- **Workflow A:** always use Enhanced Mode. Initialization does not automatically include scaffolding, license selection, remote creation, commit, or push.
- **Workflow B:** build the exact change list, then select Normal or Enhanced Mode; switch to Stop Mode for any stop condition.
- Run the same check once for the same state. Reclassify and rerun affected checks only after files, index, HEAD, branch, or remote change; another skill edits content; integration or conflict resolution occurs; substantial time passes; or an external process may have changed state.

## Completion Report

Briefly report mode and actions, branch and remote, new commit and included files, sensitive and extraneous-file inspection scope, documentation synchronization, checks that passed or were unavailable, push and local/remote consistency, and remaining changes or risks. Report completion only when authorized actions succeeded, remote consistency was verified when required, and no risk was hidden.
