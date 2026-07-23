# Enhanced Mode

Use this mode for first-time initialization or unfamiliar and higher-risk changes. This is a complete procedure and does not require Normal Mode; apply the main skill's shared baseline first.

## Expanded Inventory

- Fully inspect root, branch, HEAD, worktree, staged/unstaged/untracked/ignored files, remote/upstream, active Git operations, and task scope.
- Inspect unfamiliar, binary, large, generated, archive, database, export, backup, log, cache, coverage, build, IDE/OS metadata, and records without continuing value.
- Verify `.gitignore` covers confirmed non-source material without hiding required source. Never overwrite existing rules with a generic template.
- Prefer a repository-provided secret scanner; otherwise use filename, pattern, and semantic inspection without installing tools.
- Inspect the complete staged diff, required outgoing commits, and history exposure. Report individual sizes and suggest Git LFS only for binary or abnormal-size cases.
- Expand documentation consistency and existing verification across affected areas. Reclassify after another skill edits content and rerun only affected checks.

Never delete extraneous files automatically. List exact paths, rationale, and options to ignore, retain, remove, or relocate them, then let the user decide.

## Workflow A: First-Time Initialization

1. Inspect every regular and hidden entry. If Git exists, use Workflow B.
2. Inspect sensitive information, extraneous files, and `.gitignore`. Exclude `TODO.md`, `docs/PRD.md`, `docs/private/`, real `.env`, and confirmed generated material by default. Reconfirm suitability before publishing a PRD.
3. Default to `main` when unspecified and report the choice. Use `git init -b <branch>` or an equivalent non-destructive fallback for older Git.
4. Add a remote only after the user supplies or confirms its URL. Before creating a hosted repository, confirm platform, name, owner, and public/private visibility; never infer visibility.
5. For initialization only, stop without committing or pushing.
6. Before the initial commit, verify `user.name`, `user.email`, and signing policy without changing global configuration silently. Stage exact paths, inspect the complete staged diff and `git diff --cached --check`, then commit.
7. Query the remote once near push. With no same-name branch, `git push -u <remote> <branch>` is allowed. Unrelated remote history switches to Stop Mode.

Initialization does not imply scaffolding, license selection, remote creation, commit, or push. Never create `LICENSE`, merge unrelated history, or force-push automatically.

## Workflow B: Existing Repository

1. Build the exact file list. Propose atomic commits for unrelated purposes and let the user decide whether to split them.
2. Inspect pre-existing staged content. If it includes out-of-scope files, switch to Stop Mode; never unstage or include them autonomously.
3. Complete the expanded inventory, sensitive-information and documentation synchronization, and existing verification for every affected area.
4. Do not create an empty commit. Stage exact paths, inspect the complete staged diff and `git diff --cached --check`, then create a single-purpose commit.
5. When push is required, fetch once after content stabilizes: push normally when only ahead; set missing upstream only for an explicit upload when no same-name remote branch exists; switch to Stop Mode when behind, diverged, mismatched, or fetch fails.
6. After push, compare local HEAD with the remote-tracking branch and inspect the remaining worktree.

Never downgrade the mode to skip checks. For any stop condition, stop expanding impact and load Stop Mode immediately.
