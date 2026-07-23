---
name: manage-project-git
description: Safely and consistently manage project Git initialization, commits, and pushes. Use for a first git init, initial branch and remote setup, and the initial commit, or for inspecting an existing repository, synchronizing documentation, scanning sensitive information and extraneous files, running verification, staging exact paths, committing, and uploading. Stop on remote-version differences, conflicts, failed checks, sensitive data, pre-existing staged content, or other anomalies; report evidence and viable options, then let the user choose the resolution.
---

# Manage Project Git

Standardize first-time initialization and routine commit-and-push work. Prioritize preservation of user work, prevention of data exposure, and traceability. Never bypass verification, overwrite a remote, or rewrite history merely to complete a push.

## Core Principles

- Determine whether the user requested initialization only, commit only, push only, or commit and push. Do not expand the external change.
- Limit work to the repository and files in scope. Preserve unrelated modifications, branches, tags, remotes, and staging state.
- Inspect before staging, verify the index before committing, and compare remote state before pushing.
- Stage exact paths. Use broad add operations only after reviewing the entire worktree file by file.
- Never automatically run `reset --hard`, `clean`, discard changes, delete branches, rewrite history, amend commits, or force-push.
- When the user explicitly requested a normal commit and push, complete them consecutively after all checks pass. Stop and ask the user to choose whenever a difference, risk, or error appears.
- Secret scanning reduces risk but never proves that no sensitive information exists.
- Never echo complete tokens, passwords, private keys, or other secrets. Report only the file, category, and a minimally masked location.

## Select the Workflow

1. Use Workflow A when the directory is not a Git repository or the user explicitly requests first-time initialization.
2. Use Workflow B when Git metadata exists or a Git root can be resolved.
3. If nested repositories, submodules, worktrees, or a mismatch between the current path and requested project are detected, report the actual root and affected scope first. Stop when the target remains ambiguous.
4. If the user requests inspection or commit preparation only, stop after the pre-commit report. Do not commit or push.

## Shared Pre-Commit Checks

### 1. Inventory the repository and worktree

Identify and record:

- Git root, current branch, HEAD, worktree state, and detached-HEAD status.
- Staged, unstaged, untracked, deleted, and renamed files; inspect ignored files when relevant.
- Remote names and URLs, upstream, and the branch's ahead/behind relationship.
- Before committing, verify effective `user.name`, `user.email`, and existing signing requirements. If identity is missing or may be unsuitable for publication, stop; never change global configuration silently, and explain repository-local, global, and privacy-address options.
- Active merge, rebase, cherry-pick, revert, or bisect operations and unresolved conflicts.
- Whether pre-existing staged content belongs to this task. If the index mixes earlier user-staged files that should not enter this commit, stop and ask the user. Never unstage or include them silently.

Read `AGENTS.md`, contribution guidance, and repository-specific Git and test instructions first. Do not assume the default branch, remote name, or commit convention.

### 2. Inspect sensitive information and extraneous files

Review every tracked change and untracked file intended for the commit. For a push, also inspect the complete outgoing commit range that does not yet exist on the target remote. Include:

- `.env` files, credentials, private keys, key containers, cloud authentication, cookies, sessions, database connection strings, and URLs containing credentials.
- API keys, access tokens, passwords, secrets, and authorization headers. Prefer an existing repository secret scanner; otherwise supplement filename, pattern, and semantic inspection. Do not install a scanner automatically.
- Personal or customer data, internal endpoints, commercial plans, unpublished PRDs or TODOs, `docs/private/`, and other non-public material.
- Logs, debug output, caches, coverage, build artifacts, dependency directories, temporary files, backups, exports, databases, archives, oversized binaries, IDE/OS metadata, and record documents with no continuing reading value.
- Whether `.gitignore` covers confirmed non-source material without excluding required source files.

When a possible secret is found:

1. Stop staging, committing, and pushing.
2. Do not reveal the full value; report only the file and risk category.
3. If uncommitted, recommend removing it, using environment or secret management, and adding an appropriate ignore rule.
4. If it entered a commit or remote, explain that `.gitignore` cannot erase history. Recommend revocation or rotation first, then present history-cleanup options. Never rewrite history or force-push without explicit approval.

Do not delete extraneous files automatically. List exact paths, rationale, and options to ignore, retain, remove, or relocate them, then let the user decide.

### 3. Synchronize code, planning, and documentation

Compare code, configuration, tests, public behavior, and documentation:

- When verified features, commands, configuration, limitations, versions, or structure changed, use available `$write-project-readme` to synchronize `README.md` and `README.en.md`.
- When `docs/` contains development records, duplication, private plans, or unsuitable public material, use `$manage-project-docs` for the audit. If that skill requires approval, pause the Git workflow for the user's decision.
- When the project maintains progress in local `TODO.md` and implementation status changed, use `$write-project-todo`; preserve its ignored state and do not upload it merely because it was synchronized.
- Use `$write-project-prd` only when product requirements actually changed and the user wants them updated. Keep the PRD private and ignored by default.
- If an empty directory also needs the standard project scaffold, use `$initialize-project-structure` first. It must not initialize Git; return to Workflow A afterward.
- For broad or high-risk code changes, or when the user requests a pre-delivery review, use `$code-review` for read-only findings first. Do not expand the implementation scope automatically because of those findings.

These skills are conditional, not hard dependencies. Invoke only available skills whose trigger conditions apply. After any skill changes files, rerun worktree, sensitive-information, documentation, and verification checks.

### 4. Run quality verification

- Run the repository's documented tests, linting, formatting, build, type checks, or skill validation appropriate to the change.
- Run `git diff --check` and inspect the staged diff and scope.
- Do not install dependencies, change the toolchain, or alter code merely to conceal a failed check.
- Report missing, unavailable, and failed checks accurately. When a failure can affect commit quality, stop and let the user choose to fix it, reduce scope, or knowingly accept the risk.

## Workflow A: First-Time Initialization

### 1. Validate initialization conditions

- Inspect all regular and hidden entries, the target directory, and existing Git metadata.
- If it is already a Git repository, do not initialize again; switch to Workflow B.
- Git initialization does not imply project scaffolding, license selection, or remote-repository creation. Perform those only when separately requested.
- If no initial branch is specified, default to `main` and report that choice.

### 2. Prepare tracking boundaries

- Complete the shared sensitive-information and extraneous-file inspection before `git init`.
- Inspect or create a `.gitignore` appropriate to the actual project. Never overwrite existing rules with a generic template.
- Exclude local `TODO.md`, `docs/PRD.md`, `docs/private/`, real `.env` files, and confirmed generated material by default. Track a PRD only after the user explicitly requests publication and its content is confirmed suitable.
- Never choose or create a `LICENSE` automatically.

### 3. Initialize and configure a remote

1. Initialize with `git init -b <branch>`. If unsupported by the installed Git version, use an equivalent non-destructive initial-branch setup.
2. Verify the Git root and branch.
3. Add a remote only after the user supplies or confirms its URL. `origin` may be the default name; stop if an existing name or URL differs.
4. Before creating a GitHub, GitLab, or other hosted repository, obtain the platform, repository name, owner, and public/private choice. Remote creation is a separate external action; never infer public visibility from local content.

If initialization alone was requested, report and stop here without creating a commit or pushing.

### 4. Create the initial commit and first push

When the user also requests a commit or upload:

1. Complete all shared pre-commit checks and quality verification.
2. List included and excluded files, then stage exact paths.
3. Inspect `git diff --cached --check`, the complete staged diff, and file statistics.
4. Derive a concise commit message from actual content. Do not claim unfinished or unverified functionality.
5. Create the commit and record its hash.
6. Query the remote branch before pushing. When no same-name branch exists, a normal `git push -u <remote> <branch>` is allowed.
7. If the remote already has unrelated history, stop and offer options: inspect and integrate remote content, use a new branch and pull request, or knowingly replace the remote. Never force-push or merge unrelated histories automatically.

## Workflow B: Commit and Upload an Existing Repository

### 1. Confirm commit scope

- Derive the file set from the user request, current changes, and established task context.
- When changes serve multiple unrelated purposes, recommend atomic commits and let the user decide whether to split them.
- Do not create an empty commit unless explicitly requested for an understood purpose.

### 2. Compare remote versions

Before pushing, safely refresh remote information with a command such as `git fetch --prune`, then compare the local branch with its upstream or target remote branch:

- Local ahead and not behind: a normal push may proceed.
- Local behind: stop and offer inspect-then-rebase, merge, or defer-push options.
- Diverged: stop, report commit counts and relevant commits, then offer rebase, merge, or a new branch/pull request.
- Missing upstream: confirm the target remote and branch. Set upstream only when upload was explicitly requested and no same-name remote branch exists.
- Fetch, checks, hooks, authentication, network, LFS, branch-protection, or permission failures: preserve the concise error and current state, then offer targeted options. Never bypass them by disabling hooks, skipping checks, or force-pushing.

Never pull, merge, or rebase automatically. After the user chooses an integration strategy, recheck worktree safety before proceeding and rerun all pre-commit checks and verification after integration or conflict resolution. Stop on conflicts, list conflicted files and viable resolutions, and never guess the intended content.

### 3. Stage and commit

1. Complete shared checks, required documentation synchronization, and verification.
2. Add each in-scope path explicitly, avoiding unrelated untracked or ignored files.
3. Reinspect staged paths, content, sensitive information, file size, and `git diff --cached --check`.
4. Write a single-purpose, traceable commit message from the staged diff and follow repository conventions. When none exist, use a concise Traditional Chinese imperative or result statement.
5. Create the commit. Do not automatically amend, sign, tag, or create a release.

If a commit hook fails, report the hook and error. Rerun relevant checks after a fix. Never use `--no-verify` unless the user explicitly chooses it after understanding the risk.

### 4. Push and verify

1. Immediately before pushing, recheck HEAD, branch, remote URL, and ahead/behind state to detect changes after the earlier inspection.
2. Use a normal push. Do not automatically push other branches, tags, or all refs.
3. Stop on non-fast-forward; never retry automatically as a force-push.
4. Consider `--force-with-lease` only after the user explicitly requests remote-history rewriting, confirms the exact remote and branch, and accepts the impact. Never use bare `--force`.
5. After pushing, compare local HEAD with the remote-tracking branch and inspect the worktree again for remaining changes.

## Error Report Format

When a version difference or error appears, stop actions that would expand impact and report:

1. **Current state**: branch, HEAD, remote, ahead/behind, worktree, and completed actions.
2. **Evidence**: concise error, conflicted files, or risk category without exposing secrets.
3. **Impact**: commits, files, remotes, and collaborators that may be affected.
4. **Options**: safe choices, trade-offs, and a recommendation, including a defer option.
5. **Decision gate**: do not merge, rebase, untrack, clean history, change remotes, delete, or force-push until the user chooses.

## Completion Report

Report:

- Whether initialization, commit, push, or a combination was performed.
- Git root, branch, remote, and upstream.
- New commit message, short hash, and included files.
- Scope of sensitive-information and extraneous-file inspection plus exclusions; never claim zero risk.
- Documentation synchronization and other skills invoked.
- Checks that actually succeeded and any skipped or failed checks.
- Push result and whether local and remote commit hashes match.
- Remaining staged, unstaged, untracked, ignored, or unresolved risks.

Report completion only when every authorized action succeeded, remote consistency was verified, and remaining risks were disclosed.