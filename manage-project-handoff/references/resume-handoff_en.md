# Resume from a Handoff

Run this procedure when a new session needs to understand, inspect, or continue an existing handoff.

## 1. Read in Priority Order

Read current system, user, and project instructions first, then:

1. Applicable `AGENTS.md` files.
2. `docs/private/HANDOFF.md`.
3. Referenced `TODO.md`, `docs/PRD.md`, READMEs, decision records, and key code.
4. Configuration and tests directly relevant to the next action.

If no handoff exists, do not invent one. Reconstruct only verifiable state from PRD, TODO, Git, and repository content, and disclose that temporary context from the prior session is missing.

## 2. Verify Freshness

Inspect the current Git root, branch, HEAD, staged/unstaged/untracked files, active Git operations, and referenced paths, then compare the snapshot:

- When branch or HEAD differs, report the difference and do not assume the handoff remains applicable.
- When the worktree differs, prefer current files and mark the snapshot stale.
- Downgrade completed, blocked, or verified claims to pending confirmation when current evidence is absent.
- When a user instruction conflicts with current `AGENTS.md`, PRD, TODO, or newer direction, follow current explicit direction and report the conflict. Stop for a user decision when precedence is unclear.
- Do not inherit “tests passed” blindly. Decide whether to rerun based on continued work, state changes, and risk.

Never reset, check out, clean, or overwrite current work to match an old snapshot.

## 3. Restore User Intent

Classify handoff instructions as:

- Still active with clear scope.
- Requiring confirmation to continue.
- Superseded by current instructions or an official source.
- Conflicting with current state.

Treat only the first category as an active constraint. A durable-rule candidate not yet in `AGENTS.md` must not be expanded beyond its recorded scope. For ambiguous wording or missing expiry, use the narrowest reasonable scope and disclose the assumption.

## 4. Report the Restored State

Before implementation, briefly report:

1. Current objective and related PRD/TODO.
2. Active user instructions and their scope.
3. Verified branch, HEAD, worktree, and test state.
4. Differences, stale claims, and conflicts between handoff and current state.
5. One to three trustworthy next actions.
6. Blockers requiring a user decision.

If the user only asks to read the handoff or report current status, stop here.

## 5. Continue Work

Continue only when the user also asks to proceed:

- Use the appropriate implementation, documentation, or Git skill for the task.
- Preserve confirmed constraints and reconfirm before expanding scope.
- Rerun only verification invalidated by changes to HEAD, worktree, environment, or elapsed time.
- After material state changes, synchronize official TODO/README sources first. Run Prepare Handoff again when the user asks to switch sessions.

Never delete or clear the old snapshot automatically during resume. When the project is complete or the handoff is no longer needed, propose deletion and wait for confirmation.
