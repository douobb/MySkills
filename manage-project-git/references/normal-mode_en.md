# Normal Mode

Use this mode for a small, single-purpose change in an existing repository with no high-risk signal. Apply the main skill's shared safety and documentation baseline first.

## Procedure

1. Once, inspect the Git root, branch, HEAD, worktree, staged/unstaged/untracked files, remote/upstream, active Git operations, and task scope.
2. Inspect pre-existing staged content. If it contains out-of-scope files, switch to Stop Mode; never unstage or include them autonomously.
3. Scan only changes and files intended for the commit. For a push-only request, also inspect outgoing commits absent from the target remote.
4. Apply the sensitive-information and documentation baseline, then run only relevant tests, lint, build, or skill validation. Do not create an empty commit unless explicitly requested for an understood purpose.
5. Verify effective `user.name`, `user.email`, and signing policy without silently changing global configuration.
6. Stage exact paths and inspect staged files, the complete staged diff, and `git diff --cached --check`.
7. Create a single-purpose commit following repository convention; otherwise use concise Traditional Chinese. Do not automatically amend, sign, tag, or create a release.
8. When push is required, run `git fetch --prune` once after content stabilizes and compare the target branch:
   - Local ahead and not behind: perform a normal push.
   - Missing upstream with no same-name remote branch: an explicit upload request permits setting upstream.
   - Local behind, diverged, remote mismatch, or fetch failure: switch to Stop Mode.
9. After push, compare local HEAD with the remote-tracking branch and inspect the remaining worktree.

## Compactness and Transitions

- Do not list every normal file size, scan the entire ignored tree, run unrelated tests, or repeat checks while state is unchanged.
- A normal run needs a short starting update and a complete final report; add an update only for a material issue.
- Load Enhanced Mode for unfamiliar files, binary/large artifacts, private content, high-risk code, mixed purposes, unreviewed outgoing commits, or unclear remote/upstream state. Load Stop Mode immediately for any stop condition.
