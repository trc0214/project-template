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
