---
name: write-project-readme
description: Create, improve, review, update, or synchronize README.md and README.en.md by inspecting the repository, source code, configuration, documentation, tests, attribution, and release information. Keep both files semantically equivalent in natural Taiwan Traditional Chinese and technical English, and never invent unsupported features, commands, versions, references, licenses, or releases.
---

# Write Project README

Create or incrementally update README.md and README.en.md. README.md is the Traditional Chinese semantic source; README.en.md is its English counterpart. The skill may run when either or both files are missing, and docs/PRD.md is optional.

## Core Principles

1. **Verify before writing**: When repository content is available, do not generate a generic README from only the project name or a brief request.
2. **Use verified facts only**: Support concrete claims with source code, configuration, manifests, build scripts, tests, formal documentation, release data, user instructions, or still-accurate existing README content.
3. **Separate implementation from plans**: Treat executable code and configuration as evidence of implemented behavior. Mark PRD-only work as planned or omit it; never present it as complete.
4. **Serve new readers**: Prioritize the project's purpose, problem, current capabilities, installation or execution path, and links to further documentation.
5. **Keep both languages synchronized**: Facts, status, commands, versions, links, attribution, licenses, release information, and warnings must remain equivalent. Never update only one file.
6. **Preserve valid human content**: During incremental updates, retain accurate branding, layout, warnings, acknowledgements, and usage guidance. Change only content affected by the project or needed for clarity.

Omit unverifiable information. Mark it unconfirmed or ask the user only when it is essential and cannot be safely omitted. Never add empty sections or placeholders such as TODO or Coming soon.

## Repository Inspection

### Sources

Read both existing README files fully, then inspect as applicable:

- Source code, tests, docs/, and docs/PRD.md
- Package manifests, lockfiles, runtime/toolchain version files, and build scripts
- Containers, CI, release workflows, publishing configuration, and changelogs
- .env.example, configuration schemas, and public configuration documentation
- LICENSE, COPYING, NOTICE, CITATION.cff, AUTHORS, acknowledgement, and contribution files
- When appropriate, Git remotes, local tags, fork metadata, and source license headers

After detecting the technology stack, inspect its equivalent conventional files. Do not access private remote resources without permission.

Build an internal fact inventory that separates verified facts, implemented and planned features, uncertain or stale content, sensitive information, technology versions, release status, licenses, and upstream relationships.

### Conflict Priority

For general facts, prefer:

1. Current executable code and configuration
2. Package manifests and build scripts
3. Tests
4. The user's current explicit instructions
5. Formal documentation
6. Existing README content
7. PRD plans

For versions, prefer runtime/toolchain version files, package constraints, lockfiles, container or CI configuration, build scripts, then existing documentation. Do not infer versions from the local environment or general ecosystem knowledge, use unsupported latest labels, or alter the precision of a verified range.

For upstream and attribution relationships, prefer fork or remote metadata, source or license headers, NOTICE or CITATION.cff, user instructions, existing acknowledgements, then formal documentation. A dependency or structural similarity alone does not prove derivation, ownership, or plagiarism.

### When to Ask

Ask only when missing information materially blocks an accurate README, for example:

- The project's purpose or public name is unclear
- Multiple startup commands conflict and none can be verified
- Essential private setup instructions are missing
- Documentation materially conflicts with implementation
- A substantial upstream relationship appears likely but cannot be confirmed

Do not ask about decorative choices such as badges, emojis, or screenshots by default. Omit sections whose only missing content is minor.

## README Structure

Each README must contain:

1. A verified project title
2. A concise description of its purpose, intended context, and primary value
3. A relative link to the other language

Use [English](README.en.md) in README.md and [繁體中文](README.md) in README.en.md, with consistent placement and formatting.

Include only sections supported by evidence and useful to readers:

| English | Traditional Chinese | Inclusion rule |
|---|---|---|
| Overview | 專案簡介 | Add when the short description is insufficient or background, users, goals, context, or an important upstream relationship must be explained |
| Features | 功能特色 | List verified capabilities and describe behavior rather than internals; label incomplete work |
| Demo | 展示 | Include only existing demos, screenshots, GIFs, or videos with clear rights; prefer relative repository paths and verify capitalization |
| Requirements | 系統需求 | Include verified OS, runtime, tool, service, or hardware prerequisites; separate runtime and development needs when useful |
| Technology Stack | 使用技術 | List central technologies that aid understanding or execution; preserve verified versions and ranges, and omit transitive dependencies |
| Installation | 安裝 | Provide reproducible steps in order using the lockfile's package manager, actual scripts, paths, and required build or configuration steps |
| Configuration | 設定 | Document only settings supported by examples, schemas, code, or formal docs; identify required values and use placeholders for secrets |
| Usage | 使用方式 | Give examples matching actual CLI, UI, API, or library behavior; link detailed guidance from docs/ |
| Development | 開發 | Include verified development, build, lint, formatting, debugging, or local-service workflows that differ from ordinary usage |
| Project Structure | 專案結構 | Add only when helpful; show important paths, not dependencies, outputs, caches, or every minor file |
| Testing | 測試 | Include only when tests or test commands exist; never infer coverage or completeness |
| Documentation | 文件 | Link only existing public documents; do not expose private planning or link the Git-ignored TODO.md |
| Release | 發布版本 | Include only with formal evidence such as tags, releases, changelogs, publishing configuration, artifacts, or workflows |
| Roadmap | 開發藍圖 | Add when requested or supported by public high-level plans; never copy the full TODO.md or private tracking data |
| References | 參考與致謝 | Required for verified adaptation, port, fork, article, asset, model, dataset, paper, or other source relationships |
| Contributing | 貢獻 | Add only with formal guidance, templates, workflows, or user instructions; never invent branch, commit, PR, or review rules |
| License | 授權 | Add only when a license file, package metadata, or user instruction verifies the license; otherwise usually omit |

Do not create Overview when the title description is sufficient. Keep detailed architecture, API, database, and deployment material in docs/ unless a short summary is necessary. Badges are not a section; add only a few whose targets and values are verified and useful.

## Critical Content Rules

### Commands, Versions, and Configuration

- Derive installation, startup, build, test, and development commands from project files and preserve their order. For example, do not replace pnpm with npm when pnpm-lock.yaml is authoritative.
- Preserve the supported precision of versions, whether a major version, minimum, exact lock, or range. Omit or identify an unpinned version when it cannot be determined.
- Never invent supported platforms, compatibility, API endpoints, output, performance claims, or security guarantees.
- Never copy real .env values, tokens, passwords, private keys, personal paths, or private endpoints. Use placeholders such as API_KEY=your_api_key.

### Attribution, License, and Releases

When the project is materially forked, derived, or adapted from an identifiable repository:

1. Disclose the relationship accurately and link it early in Overview.
2. Direct readers to References.
3. In References, record the source name and link, relationship type, main modifications, and relevant license or attribution requirements.

Use precise relationship wording: Based on means substantial implementation or structure is derived; Forked from means an actual fork or continuation; Adapted from means selected code, design, or concepts were modified; Inspired by means the implementation is substantially independent; Uses means the source is a library, tool, asset, dataset, or service. Do not weaken a substantial adaptation or use different-strength wording between languages.

If a license is unverified, do not claim MIT, Apache, GPL, open-source, or proprietary status, and do not select or create a license. If attribution requirements are unclear, state that further license review is required.

Release content must come from verified versions, dates, links, artifacts, and status. Never invent a latest version, download link, or automatic-update support, and never describe a default branch or prerelease as stable.

## Writing and Synchronization

- Write README.md in natural Taiwan Traditional Chinese. Preserve commands, paths, identifiers, and code, and avoid vague promotional language.
- Write README.en.md in natural technical English rather than a mechanical word-for-word translation.
- Keep section scope and facts equivalent. Commands, versions, URLs, filenames, and release identifiers should normally be identical.
- If one file contains additional accurate information, verify it before synchronizing it into both files.
- Update existing README files incrementally: classify accurate, stale, unsupported, duplicated, and single-language content; remove broken links and stale commands without deleting valid custom content merely because it differs from a generic template.

## Workflow

1. **Inspect the repository**: Read relevant code, configuration, tests, documentation, attribution, release data, and both README files.
2. **Build a fact inventory**: Separate verified, planned, uncertain, stale, and sensitive information.
3. **Select sections**: Keep only evidence-backed content that helps readers.
4. **Draft the Chinese version**: Establish the shared meaning in README.md.
5. **Synchronize English**: Update README.en.md from the Chinese content and the same facts; add no English-only information.
6. **Validate content**: Inspect or safely execute commands and verify paths, filenames, links, configuration, versions, attribution, releases, and downloads. Never modify the project merely to fit README claims.
7. **Compare languages**: Confirm matching sections, facts, status, warnings, and attribution strength.
8. **Report results**: Summarize files and major sections changed, omitted unsupported information, important open questions, license, upstream, and release detection, and whether commands were actually tested.

Report a command as tested only when it was executed successfully.

## Completion Check

Before completion, confirm:

- Both README files exist, link to each other, and use natural Traditional Chinese and English.
- Project title, description, sections, features, and status are semantically synchronized.
- Every concrete claim has evidence, and planned work is not presented as complete.
- Commands, paths, filenames, relative links, configuration, and versions are correct and consistent.
- No secrets, empty sections, placeholders, broken links, or unsupported feature, compatibility, license, or release claims remain.
- Valid human content, attribution, license notices, and important upstream relationships are preserved.
- Material upstream relationships are disclosed early in Overview and detailed in References.
- Optional Release, License, Contributing, Testing, Demo, and badge content has evidence.
- Markdown headings, tables, and code fences are valid.

Do not delete unrelated files, modify source code to fit the documentation, or stage, commit, or push changes unless explicitly requested.

The task is complete only after these checks pass and the verified scope is reported.
