# AI Agent Repository Guidelines

## Scope and precedence

This file is the repository-level baseline for AI agents. Apply instructions in this order:

1. The user's explicit instructions for the current task.
2. This repository's `AGENTS.md` and any more specific instructions in scope.
3. The governing `DEVELOPMENT_GUIDELINES` from the originating workspace, when available.
4. Other workspace rules.
5. Tool defaults.

Project maintainers may make this file stricter or override this baseline for project needs. In particular, document project-specific test, lint, type-check, build, deployment, protected-file, architecture, ownership, and scope rules here.

## Repository governance

GitHub and this Git repository are the canonical source for source code, branches, commits, issues, pull requests, and implementation state. Chat transcripts must never be the only record of project state.

The default base branch is `main`. Keep `main` stable and deliverable. Humans and AI agents should not perform feature development directly on `main`; use a task branch and a pull request.

## Branches

Name AI-agent branches `ai/<agent>/<task>`, for example:

- `ai/chatgpt/auth-api`
- `ai/claude/auth-tests`
- `ai/gemini/dashboard-ui`

Use `feature/<task>`, `fix/<task>`, `docs/<task>`, `refactor/<task>`, `test/<task>`, or `chore/<task>` for general work. A branch represents a task, not an agent. Do not maintain permanent branches named only after agents, such as `chatgpt`, `claude`, or `gemini`.

Before starting work, confirm the current branch, base branch, task goal, allowed and prohibited scope, acceptance criteria, and repository-specific instructions. Synchronize with a reasonably current base branch before implementation.

## Existing project intake

When joining a project after implementation has already started—including taking over an existing repository, handoff, incomplete PR, or long-running maintenance task—complete a project intake before modifying code. Do not start from a chat summary, a single README, or a preferred architecture pattern alone.

Before implementation, at minimum:

1. Read `AGENTS.md`, `README`, `CONTRIBUTING`, relevant `docs/`, ADRs or decision records, and any repository-to-workspace mapping that exists.
2. Confirm the default/base branch, active branches, open PRs and issues, recent relevant commits, current owner, and handoff state.
3. Understand the current entry points, module or service boundaries, data flow, external dependencies, configuration, storage, deployment path, and important security boundaries.
4. Inspect `git status` and the relevant diff. Run the existing tests, lint, type checks, and build when reasonably possible to establish a baseline. Record existing failures as pre-existing rather than attributing them to the new task.
5. Identify ongoing migrations, deprecated components, technical debt, known risks, protected files or areas, and concurrent work by other agents or contributors.
6. Reconfirm task scope, prohibited scope, acceptance criteria, and ownership before editing implementation.
7. If documentation and implementation disagree, treat verifiable repository state as authoritative for implementation and record the documentation drift in an issue, PR, or durable project document.

For non-trivial work, leave a concise Current State summary in an issue, PR, handoff, or other durable context. Do not refactor merely because the current architecture differs from personal or model preference. Improvements outside the assigned scope should be proposed separately and evaluated under the architecture-change process below.

## Multi-agent ownership

One primary owner should implement a given task at a time. Other agents may review, research, test, document, or own clearly separated subtasks. Do not independently rewrite the same implementation on another branch unless the task explicitly compares alternatives. When agents work concurrently, separate file ownership or functional boundaries wherever practical.

## Pull requests

Merge agent branches through pull requests. Keep every PR single-purpose. Its description must include:

- Summary
- Scope
- Important design decisions
- Verification
- Known risks
- Follow-up or handoff information

Before merge, confirm that the branch is reasonably synchronized with its base; applicable tests, lint, type checks, and builds pass; and the diff contains no secrets, debug artifacts, unexpected files, or out-of-scope changes.

## Commits and AI metadata

Use Conventional Commits with `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, or `build`. Avoid messages without useful intent, such as `update`, `changes`, `test`, or `fix stuff`. Commit at meaningful, understandable state boundaries rather than after every tiny edit.

AI-led commits should include these trailers when practical:

```text
AI-Agent: <agent/model>
Issue: #<issue-number> | N/A
Work-State: In-Progress | Checkpoint | Resolved
Problem: <goal or problem>
Verification: <tests/lint/build performed>
```

When taking over prior AI work, optionally add `Handoff-From: <agent/model or commit SHA>`.

Work states mean:

- `In-Progress`: an atomic development change while the task remains incomplete.
- `Checkpoint`: a preserved handoff state before an agent/model switch, session end, or major change of approach.
- `Resolved`: acceptance criteria and reasonable verification are complete. GitHub issue and PR lifecycle still determines closure.

Do not use `Closes #N`, `Fixes #N`, or `Resolves #N` for partial fixes, checkpoints, or unreviewed work. Use a closing keyword only when merge should truly close the issue. For multi-commit work, prefer `Closes #N` in the final PR description.

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

Never hand off with only a vague instruction such as “continue” or “finish this.”

Before switching agents or models: organize the working tree, remove debug and temporary artifacts, run reasonable checks, create a checkpoint commit, push the branch, and update the issue, PR, and handoff. The receiving agent must review `AGENTS.md`, the current branch, recent commits, issue or PR, handoff, `git status` and diff, and current test status. A chat summary alone is insufficient.

## Major technical decisions and architecture changes

Routine changes may be decided by the task owner when they remain inside the approved scope and do not alter external contracts, data integrity, security models, deployment topology, or canonical-source boundaries. Examples include implementation details, local refactors, naming, internal organization, and low-risk dependency updates.

Treat the following as significant changes unless repository-specific rules say otherwise:

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

Before implementing a significant change:

1. Create a recoverable checkpoint that preserves the verified pre-change state.
2. Record a decision proposal in an ADR, decision document, issue, or PR proposal. Include Current State, Problem / Motivation, Alternatives Considered, Recommended Option, Impact / Blast Radius, Migration Strategy, Rollback Strategy, and Testing / Verification Plan.
3. Record the decision owner and approval status. An AI agent must not self-approve changes that materially affect external behavior, data integrity, the security model, deployment topology, canonical source, core architecture, or an irreversible/high-cost operation. Obtain explicit user or maintainer approval first.
4. Do not hide an architecture change inside an ordinary feature or bug-fix PR. Prefer a separate PR; if separation is impractical, clearly isolate the architecture change and link the approved decision record.
5. Prefer incremental, verifiable, reversible migrations. If rollback is impossible, document the irreversible risk and recovery plan before execution.
6. After implementation, update relevant architecture, README, `AGENTS.md`, ADR/decision, API/schema/deployment documentation, and issue/PR state so durable context matches the actual implementation.

Decision authority principle: AI agents may decide implementation details within an approved architecture and task scope. For significant direction changes, their role is to propose, compare, validate, and implement an approved option—not to assume architecture governance authority. When uncertain whether a change is significant, propose first and do not change the architecture by default.

## Testing and dependencies

Prioritize tests for core logic, data transformations, authorization, security boundaries, and regression-prone behavior. Add a regression test for an important bug when reasonably possible.

Before submitting a PR, run the project's documented test, lint, type-check and build commands when available. Add the actual commands to this file after choosing the project's technology stack; do not invent commands.

Use the language ecosystem's standard machine-readable dependency manifest and lockfile. Do not list dependencies only in README documentation.

## Secrets

Never commit API keys, passwords, access tokens, private keys, service-account credentials, production secrets, or a real `.env`. `.env.example` may contain safe placeholders only.

If a secret enters Git history, deleting the current file is not enough. Treat the secret as compromised, rotate it, and clean Git history where appropriate.

## Documentation and generated content

README documentation should cover purpose, setup, configuration, development, and—when applicable—architecture and deployment. Record important architecture decisions in an ADR, `DECISIONS` document, issue, or PR. Do not turn the README into a large collection of temporary TODOs.

For content synchronized between GitHub and another system such as Google Drive, explicitly identify the canonical source and synchronization direction. Do not create an unmanaged, manually edited two-way copy.
