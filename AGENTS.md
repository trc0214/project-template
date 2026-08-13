# AI Agent Repository Guidelines

## Scope and precedence

This file is the repository-level baseline for AI agents. Apply instructions in this order:

1. The user's explicit instructions for the current task.
2. This repository's `AGENTS.md` and any more specific instructions in scope.
3. The governing workspace development rules, when available.
4. Other workspace rules.
5. Tool defaults.

Project maintainers may make this file stricter or override this baseline for project needs. Keep project-specific test, lint, type-check, build, deployment, protected-file, architecture, ownership, and scope rules here.

## Repository governance

GitHub and this Git repository are the canonical source for source code, branches, commits, Discussions, Issues, pull requests, reviews, checks, and implementation state. Chat transcripts must never be the only record of project state.

Keep `main` stable and deliverable. Humans and AI agents should not perform feature development directly on `main`; use a task branch and a pull request.

Do not create custom governance documents when GitHub already provides a native object for the same purpose. Prefer:

- GitHub Discussions for significant architecture deliberation and the final decision summary.
- GitHub Issues for approved implementation work and acceptance criteria.
- Pull Requests for implementation review and verification.
- `README.md`, `AGENTS.md`, and when useful `CONTRIBUTING.md` for stable repository instructions.

## Branches

Name AI-agent branches `ai/<agent>/<task>`, for example:

- `ai/chatgpt/auth-api`
- `ai/claude/auth-tests`
- `ai/gemini/dashboard-ui`

Use `feature/<task>`, `fix/<task>`, `docs/<task>`, `refactor/<task>`, `test/<task>`, or `chore/<task>` for general work. A branch represents a task, not an agent. Do not maintain permanent branches named only after agents.

Before starting work, confirm the current branch, base branch, task goal, allowed and prohibited scope, acceptance criteria, and repository-specific instructions. Synchronize with a reasonably current base branch before implementation.

## Existing project intake

When joining a project after implementation has already started—including an existing repository, handoff, incomplete PR, or maintenance task—complete an intake before modifying code. Do not start from a chat summary, a single README, or a preferred architecture pattern alone.

Before implementation, at minimum:

1. Read `AGENTS.md`, `README.md`, `CONTRIBUTING.md` when present, necessary `docs/`, and relevant GitHub Discussions, Issues, and Pull Requests.
2. Confirm the default/base branch, active branches, open PRs and Issues, recent relevant commits, current owner, and handoff state.
3. Understand relevant entry points, module or service boundaries, data flow, external dependencies, configuration, storage, deployment path, and security boundaries.
4. Inspect `git status` and the relevant diff. Run existing tests, lint, type checks, and build when reasonably possible to establish a baseline. Record existing failures as pre-existing.
5. Identify ongoing migrations, deprecated components, technical debt, known risks, protected files or areas, and concurrent work.
6. Reconfirm task scope, prohibited scope, acceptance criteria, and ownership before editing implementation.
7. If documentation and implementation disagree, treat verifiable repository state as authoritative for implementation and record documentation drift in an Issue or PR when it matters.

Do not refactor merely because the current architecture differs from personal or model preference. Improvements outside scope should be proposed separately.

## Multi-agent ownership

One primary owner should implement a given task at a time. Other agents may review, research, test, document, or own clearly separated subtasks. Do not independently rewrite the same implementation on another branch unless the task explicitly compares alternatives.

## Pull requests

Merge task branches through pull requests. Keep every PR single-purpose. Use the repository PR template and GitHub's native review/check surfaces.

Before merge, confirm that the branch is reasonably synchronized with its base; applicable tests, lint, type checks, and builds pass; and the diff contains no secrets, debug artifacts, unexpected files, or out-of-scope changes.

## Commits and AI metadata

Use Conventional Commits with `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, or `build`. Commit at meaningful state boundaries rather than after every tiny edit.

AI-led commits should include these trailers when practical:

```text
AI-Agent: <agent/model>
Issue: #<issue-number> | N/A
Work-State: In-Progress | Checkpoint | Resolved
Problem: <goal or problem>
Verification: <tests/lint/build performed>
```

When taking over prior AI work, optionally add `Handoff-From: <agent/model or commit SHA>`.

Do not use `Closes #N`, `Fixes #N`, or `Resolves #N` for partial fixes, checkpoints, or unreviewed work. Prefer a closing keyword in the final PR when the merge should actually close the Issue.

## Handoff and agent switching

An incomplete-task handoff must record:

```text
Goal
Current Branch
Completed
Remaining
Files Changed
Verification
Known Issues / Risks
Recommended Next Step
```

Before switching agents or models: organize the working tree, remove debug and temporary artifacts, run reasonable checks, create a checkpoint commit, push the branch, and update the relevant Issue or PR. The receiving agent must review repository state rather than rely only on a natural-language handoff.

## Major technical decisions and architecture changes

Routine implementation details may be decided by the task owner when they stay inside approved scope and do not materially change external contracts, data integrity, security models, deployment topology, canonical-source boundaries, or core architecture.

Treat these as significant changes unless project-specific rules say otherwise:

- major module or service-boundary changes
- public API or contract breaking changes
- destructive database or schema migrations
- authentication, authorization, or security-model changes
- framework, language, runtime, or core-platform migrations
- storage-strategy or canonical-source changes
- deployment or infrastructure-topology changes
- major dependency upgrades with breaking changes
- removal of core capabilities
- large cross-cutting refactors or migrations

### Architecture Discussion

When GitHub Discussions are enabled, start a significant change in the open-ended `Architecture` category using the repository Discussion form.

The Discussion should contain only information that materially helps the decision. At minimum cover:

- problem and context
- current architecture
- decision drivers / constraints
- proposed architecture
- credible alternatives
- impact / blast radius
- open questions
- repository evidence
- required approver

When the proposal changes repository, package, module, service, or component structure, also show the target file/module structure or relevant data flow. Migration, rollback, security, performance, and test strategy are required only when they are materially affected; otherwise state `N/A` rather than inventing detail.

AI reviewers participate directly through Discussion comments or replies. Each review should identify the model, position (`Support`, `Support with Changes`, `Oppose`, or `Need More Evidence`), material concerns, repository evidence, and recommendation. Reviewers must independently inspect repository evidence and distinguish facts from inference or preference.

Multi-AI review is advisory, not a vote. AI agents must not self-approve significant changes that require user or maintainer approval.

When discussion converges, update the Discussion body or add a clear final decision comment containing:

- selected direction
- important rejected alternatives
- rationale
- accepted risks
- approver

The GitHub Discussion itself is the canonical decision record. Do not create a separate ADR, decision ledger, or AI review report unless this project explicitly requires one.

If Discussions are unavailable, an Issue may temporarily host the same deliberation. Do not create a parallel custom decision-document system as a fallback.

### Implementation Issues

After approval, create one or more implementation Issues using the native Issue Form. An implementation Issue should answer what must be done and what counts as complete; it must not reopen the architecture debate.

Use the Issue for:

- related Architecture Discussion
- implementation scope and out-of-scope boundaries
- acceptance criteria
- implementation plan
- dependencies / sequencing
- risks
- verification expectations

Split large changes into smaller Issues or sub-issues when useful. Add migration or rollback work only to Issues that actually own that work.

### Implementation Pull Requests

A PR should describe the actual implementation and verification, not repeat the Discussion rationale or the entire Issue plan. Link the relevant Issue and, for significant changes, the approved Architecture Discussion.

Use GitHub's native reviewers, review comments, Checks, Files changed view, linked Issues, labels, Projects, and milestones where useful instead of duplicating those capabilities in custom documents.

Before implementing a significant change:

1. Create a recoverable checkpoint preserving the verified pre-change state.
2. Complete the Architecture Discussion and obtain required approval in that Discussion.
3. Create implementation Issue(s) with clear acceptance criteria.
4. Implement through focused task branches and PRs linked to the Issue and Discussion.
5. Prefer incremental, verifiable, reversible migration. If rollback is impossible, record that risk in the Discussion or responsible Issue before execution.
6. After implementation, update only the stable documentation that is actually affected, such as `README.md`, `AGENTS.md`, API/schema/deployment docs, and GitHub lifecycle state.

Decision authority principle: AI agents may decide implementation details within an approved architecture and scope. For significant direction changes, their role is to propose, compare, validate, and implement an approved option—not to assume architecture governance authority.

## Testing and dependencies

Prioritize tests for core logic, data transformations, authorization, security boundaries, and regression-prone behavior. Add a regression test for an important bug when reasonably possible.

Before submitting a PR, run the project's documented test, lint, type-check, and build commands when available. Add real commands to this file after choosing the project's technology stack; do not invent them.

Use the language ecosystem's standard machine-readable dependency manifest and lockfile.

## Secrets

Never commit API keys, passwords, access tokens, private keys, service-account credentials, production secrets, or a real `.env`. `.env.example` may contain safe placeholders only.

If a secret enters Git history, treat it as compromised, rotate it, and clean history where appropriate.

## Documentation and generated content

`README.md` should cover purpose, setup, configuration, development, and—when applicable—architecture and deployment. Keep long-lived agent instructions in `AGENTS.md`. Keep TODOs and executable work in GitHub Issues rather than adding custom tracking files.

For content synchronized between GitHub and another system, explicitly identify the canonical source and synchronization direction. Do not create an unmanaged, manually edited two-way copy.
