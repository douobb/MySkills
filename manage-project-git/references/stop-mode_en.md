# Stop Mode

Use this mode for secrets, version differences, conflicts, failures, or any condition requiring a user decision. Do not change Git state until the user selects an option and the safe scope is rechecked.

## Triggers

- Possible credentials, tokens, private keys, personal data, internal endpoints, commercial plans, or other non-public content.
- `TODO.md`, `docs/PRD.md`, or `docs/private/` is tracked, staged, or present in an outgoing commit without exact publication authorization.
- Pre-existing staged content includes files outside this task.
- Detached HEAD, an active merge/rebase/cherry-pick/revert/bisect, unresolved conflicts, or an uncertain target branch.
- Material test, lint, build, hook, or skill-validation failure.
- Remote/upstream mismatch, local behind or diverged state, or unrelated remote history.
- Fetch, authentication, network, LFS, protected-branch, permission, non-fast-forward, hook, or push error.

## Immediate Response

1. Stop staging, committing, pushing, and every action that expands impact. Preserve the worktree, index, branch, remote, and history.
2. Never unstage, delete, clean, pull, merge, rebase, change a remote, bypass hooks, rewrite history, or force-push autonomously.
3. Collect the minimum evidence needed for a decision without exposing complete secret values or unnecessary sensitive content.

## Secret Response

- Report only the file, approximate location, and risk category, never the complete value.
- For uncommitted content, recommend removal, environment or secret management, and an appropriate ignore rule first.
- If content entered a commit or remote, explain that `.gitignore` cannot erase history. Revoke or rotate first, then present history-cleanup options.
- Never rewrite history or force-push without explicit approval.

## Versions, Errors, and Options

- Local behind: offer information gathering, rebase, merge, new branch/pull request, or defer with trade-offs.
- Diverged: explain commits on each side and collaborator impact, then offer rebase, merge, or new-branch options.
- Unrelated history or remote/upstream mismatch: list current and expected values, then offer correcting the remote, a new branch/repository, or confirmed integration.
- Verification, hook, authentication, permission, or network errors: report the failed stage, concise error, and safe repairs; never bypass with `--no-verify`.
- Conflicts: list files and operation state without guessing content resolution.

Consider `--force-with-lease` only after the user explicitly requests rewriting the exact remote branch and accepts the impact. Never use bare `--force`.

## Report and Recovery

1. Report branch, HEAD, remote, ahead/behind, worktree, and completed actions.
2. Explain the concise error, conflict, or risk and potentially affected files, commits, remotes, and collaborators.
3. Provide safe options, key trade-offs, a recommendation, and defer; explicitly wait for the user's choice.
4. Approval for one remedy authorizes only that remedy.
5. After repair or integration, recheck worktree, index, HEAD, branch, remote, and risk mode; load the applicable mode and rerun affected checks.
