---
name: initialize-project-structure
description: Initialize an empty directory with a minimal, technology-agnostic project structure containing blank Chinese and English README files, PRD and TODO files, documentation and source directories, a Git placeholder, and a generic .gitignore that always excludes TODO.md. Use only for empty-directory initialization; never modify an existing project, generate code, install packages, or initialize Git.
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
src/.gitkeep
```

Do not create `docs/.gitkeep`; `docs/PRD.md` already preserves the directory.

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
3. Create `.gitignore` with exactly this generic content:

```gitignore
# Local project planning
TODO.md

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

`TODO.md` must appear as an exact standalone rule. Do not ignore `README.md`, `README.en.md`, `docs/`, `src/`, or `.gitignore`, and do not add language- or framework-specific rules.

### 3. Verify the result

Confirm that:

- Every required directory and file exists.
- Every required file except `.gitignore` is zero-length.
- `.gitignore` contains the standalone `TODO.md` rule.
- No unrequested entry was created and no existing content was modified.

If `.git/` already existed and Git is available, optionally run:

```bash
git check-ignore TODO.md
```

Do not initialize Git only to perform this check.

### 4. Report

On success, show the required structure and confirm the blank files, `TODO.md` ignore rule, and absence of technology-specific content. You may suggest populating the files with README, PRD, or TODO skills, or selecting a license before public distribution; do not perform those follow-up actions automatically.

On failure, list the existing entries and state that nothing was modified to avoid mixing with or overwriting an existing project.

## Safety Boundaries

- Do not clear the directory with destructive or reset commands such as `rm`, `Remove-Item`, `git clean`, or `git reset --hard`.
- Do not choose a language, framework, or license, and do not create package manifests, technical configuration, source code, or an empty `LICENSE`.
- Do not install dependencies, initialize Git, or stage, commit, or push files.
- Create `LICENSE` only when the user explicitly requests or selects its terms.

## Acceptance Criteria

The task is complete only after the directory was validated first, the complete required structure was created, all blank files and `.gitignore` match the specification, no existing content was modified, and the result was verified and reported.
