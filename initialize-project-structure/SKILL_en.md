---
name: initialize-project-structure
description: Initialize an empty directory with a minimal, technology-agnostic project structure containing blank Chinese and English README files, PRD and TODO files, documentation and source directories, Git placeholders, and a generic .gitignore that excludes TODO.md and docs/PRD.md by default. Use only for empty-directory initialization; never modify an existing project, generate code, install packages, or initialize Git.
---

# Initialize Project Structure

Create files and directories only. Do not write README, PRD, TODO, source-code, or technology-specific content.

## Required Structure

Create this structure in the current working directory:

```text
.
├── README.md
├── README.en.md
├── TODO.md
├── .gitignore
├── docs/
│   ├── .gitkeep
│   └── PRD.md
└── src/
    └── .gitkeep
```

Except for `.gitignore`, the following files must be zero-length. Do not add headings, comments, templates, placeholders, or whitespace:

```text
README.md
README.en.md
TODO.md
docs/PRD.md
docs/.gitkeep
src/.gitkeep
```

`docs/.gitkeep` preserves the `docs/` directory while `docs/PRD.md` is excluded from Git.

## Workflow

### 1. Validate the current directory

Treat the current working directory as the project root. Do not create a nested project directory unless explicitly requested.

Before creating anything, inspect all entries, including hidden entries. Only these existing metadata items are allowed:

```text
.git/
.DS_Store
Thumbs.db
desktop.ini
```

Treat every other entry as meaningful existing content. If any exists:

1. Stop immediately without creating anything.
2. Do not overwrite, delete, move, or rename existing entries.
3. Report the blocking entries and state that the directory is not empty.

On repeated invocation, a previously generated structure also counts as existing content; do not modify or reset it.

### 2. Create the structure

After validation succeeds, complete all of the following:

1. Create `docs/` and `src/`.
2. Create all required blank files.
3. By default, create `.gitignore` with this generic content:

```gitignore
# Local project planning
TODO.md
docs/PRD.md

# Environment variables and local secrets
.env
.env.*
!.env.example

# Operating-system metadata
.DS_Store
Thumbs.db
desktop.ini

# Editor temporary files
*.swp
*.swo
*~
*.tmp
*.temp

# Logs
*.log

# Generic generated output
dist/
build/
coverage/
.cache/
```

`TODO.md` and `docs/PRD.md` must appear as exact standalone rules to prevent internal tasks, product plans, or commercial information from entering a public repository accidentally. Omit the `docs/PRD.md` rule only when the user explicitly states in the initialization request that the PRD should be version-controlled or uploaded; never infer an intent to publish it. `TODO.md` must still be excluded.

Do not ignore `README.md`, `README.en.md`, the entire `docs/` directory, `src/`, `.gitignore`, or `docs/.gitkeep`, and do not add language- or framework-specific rules.

### 3. Verify the result

Confirm that:

- Every required directory and file exists.
- Every required file except `.gitignore` is zero-length.
- `.gitignore` contains the standalone `TODO.md` rule and, by default, the standalone `docs/PRD.md` rule.
- `docs/.gitkeep` is not ignored and can preserve `docs/` while the PRD is excluded.
- No unrequested entry was created and no existing content was modified.

If `.git/` already existed and Git is available, optionally run:

```bash
git check-ignore TODO.md docs/PRD.md
```

Do not initialize Git only to perform this check.

### 4. Report

On success, show the required structure and explicitly state that `TODO.md` and `docs/PRD.md` are excluded by `.gitignore` by default and will not be uploaded by ordinary Git commits, while `docs/.gitkeep` preserves the empty documentation directory. If the user explicitly requested PRD tracking, state that the PRD is not excluded but `TODO.md` remains local-only. Also confirm the blank files and absence of technology-specific content. You may suggest populating the files with README, PRD, or TODO skills, or selecting a license before public distribution; do not perform those follow-up actions automatically.

On failure, list the existing entries and state that nothing was modified to avoid mixing with or overwriting an existing project.

## Safety Boundaries

- Do not clear the directory with destructive or reset commands such as `rm`, `Remove-Item`, `git clean`, or `git reset --hard`.
- Do not choose a language, framework, or license, and do not create package manifests, technical configuration, source code, or an empty `LICENSE`.
- Do not install dependencies, initialize Git, or stage, commit, or push files.
- Create `LICENSE` only when the user explicitly requests or selects its terms.

## Acceptance Criteria

The task is complete only after the directory was validated first, the complete required structure was created, all blank files and `.gitignore` match the specification, no existing content was modified, and the Git tracking status of both TODO and PRD was explicitly reported.
